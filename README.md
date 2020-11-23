# Shortly: Why this tick-tock based solution for Timer smart contract is the best?

**Correct economical model**

It is easy to mess up with free storage and computation provided for special contracts. For instance if scheduler will not charge for storage, such scheduler will be exploitable: contracts may use it as free storage unit. Here we paid special attention to economical model to not create a loopholes. That way contract correcly charges for storage and also check outgoing message for correct amounts. Thus, it is already suitable for work not only with grams, but also with native tokens.

**It is most general**

It works with TON primitives: messages and cells; thus is compatible with all languages and frameworks (even not developed ones).


**It is the most optimized solution (of those based on tick-tock mechanism).**

Since tick-tock transactions execute on EVERY block by main validators set, its perfomance directly affect stability and speed of the network. THus it is especially important to optimize computations in special contracts. We spend a huge efforts to optimize computations and developed contract in close to assembler low-level language.


==========================================
# Problem
In general, there are no schedulers in TON; one cannot ask a contract to execute some code in a year or 5 blocks later, etc. 
It is possible to make a third-party service off-chain that will pull specified contract on schedule, but reliability is always in question.
In Ethereum, this problem is unsolvable onchain, but TON is different. 

# Solution: specific scheduler
There is special contracts which can be customized to be executed by validators on each masterchain block.

### General vs special scheduler
General scheduler which spends gas for work may be quite expensive. However anybody can deploy one without cooperation with anybody else. Alternative solution which based on tick-tock special contracts is available in the other repository. While special contract soultion doesn't require gas for work, it however requires cooperation of validators to instantiate such contract. Thus while both solutions have pros and cons they are not mutually exclusive: both are suitable for their niches.

# Detailed scheme
1. Smart contract invoked on each block (at the start or the end). 
2. If there are messages which are ready to be send, scheduler sends them.
3. If scheduler recieve message from the other contract it treats that message as request for scheduling. It reads time for scheduling and message to be sent. Then it rewrites message to be sent and sets correct gram and native token amounts and store in the table.


# Why FunC?
There are bunch of languages and compillators supported by TON Labs which are more cosy and pleasant for developing complex smartcontracts. Why develop this contract in FunC? The pleasure of working with high-level languages comes at a price:

1. Direct load on the network: FunC are close to bare metal and thus allows unimaginable for other languages optimizations. Since scheduler constantly loads the masterchain validators - it is very important.
2. Generality. This solution works with native TON primitives such as messages and cells. It doesn't depends on Solc ABI etc. It means that proposed solution will work both with C, Solc and other codebases. And even will work with languages which are not yet developed. It is quite hard to achieve the same level of generality using high-level languages.




