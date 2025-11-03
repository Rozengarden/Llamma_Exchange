# [WIP] Llama_Exchange_Strategy

___

/!\ This is an invite to participate in a game theory reflection, and shouldn't be interpreted as financial advice.
___

## Abstract

NFTStrategies from Tokenwork have been picking up in popularity recently (with my writing speed the fad might be dead by the time you read this line). After a not so brief introduction to the subject we will discuss the specificity of The Llamas collection and how they can impact the working of the original design. This will be followed by the introduction of alternative designs that makes use of those specificity, how different token model could enhance it and the possible upsides and downsides. Finally a section will be dedicated to some of the implementation details and possible hurdles.
___

## Introduction

### What's the Strategy ?

If you are familiar with Bitcoin you might have heard of [MicroStrategy](https://en.wikipedia.org/wiki/MicroStrategy) the company funded by Michael Sailor which is accumulating Bitcoin en masse. This is done by various way, including debt backed by convertible share (I will not pretend I know what it means). As the share price went up a lot, other company followed suite, using diverse means (debt, convertible or not, spare cash, etc) to acquire crypto (mainly bitcoin, ETH for some, and sometime SOL) and add it to their treasury. Those company are referred  as Digital Asset Treasury (abbreviated DAT), but many adopted the word “Strategy" as part of their branding culminating with [MicroStrategy renaming as Strategy earlier this year](https://www.strategy.com/press/microstrategy-is-now-strategy_02-05-2025).

Coming back full circle DeFi protocols started to appear using the "Strategy" branding, some like [ETH Strategy](https://x.com/eth_strategy) taking the convertible share concept to the letter, other taking more liberties. The one of interest for today, [TokenWorks](https://x.com/token_works)'s product: NFTStrategy is on the looser side.

### NFTStrategy

Starting with the CryptoPunks collection in early September the design was as follow (this is a simplified explanation, some fee are redirected to the team, etc):

1. Create a token and put all the liquidity in a token/ETH pool on UNIv4 with a 10% fee
2. As peoples buy the token the protocol who own a huge chunk of the supply of token will start to accrue fee in ETH
3. Those fees are than used to buy an NFT from the collection
4. The NFT is then relisted at 1.2 times the price it was bought at
5. When said NFT is sold the proceed of the sale is used to buy back and burn the token from step 1. This provide the incentive for people to buy the token in step 2, sustaining the flywheel.

This initial attempt was met with success leading to the creation of spin-off for various other collection and ERC20 by the original team (funneling a part of the fee into the original punk strategy and the collection owner), but also by other team [with various degree of success](https://x.com/0xz80/status/1972731977355698452). You can even find a Strategy accumulating the cryptopunk strategy token, and another one accumulating the token of the strategy accumulating token from PunkStrategy.

### The Llamas

[The Llamas](https://x.com/WenLlama) is an NFT collection with 1111 token, but unlike most collection the money raised trough the sell in an auction have been used to create a treasury, mainly centered around the [Curve](https://x.com/CurveFinance) ecosystem, this treasury has been grown during the past years and now a portion of the yield generated every month is passed to the NFT owners.

This is done trough a contract called [The Locker](https://locker.thellamas.io/). Every NFT that are in the locker at the time of the monthly distribution will receive an equal portion of it. Llamas in the locker can only be pulled out during a 7 days period every 28 days.

This design has two main impact on the collection:

- Llama are yield generating assets, they magically make money on their own
- This has greatly diminished the amount of NFT from the collection listed on exchange platform (19 at the time of writing, slightly up from ATL due to OPEN snapshot) as peoples seems to quite like the deal of getting $40 (or 25$ during uptober) a month for some restriction on liquidity.

## Impact on a potential Strategy

Those features allow us to explore a totally different design space than the original as we don't need to rely on external factor to generate money to sustain the flywheel also isolating the protocol from their fluctuating nature. By simply locking the NFT the protocol can be self sufficient. Furthermore due to the low liquidity mentioned earlier it seems far easier to induce a supply crunch by locking llamas forever rather than relisting them at a higher price (which as far as I'm concerned a more important goals than allowing peoples to gamble on a memecoin with marginal utility).

### Drawbacks

Before exploring this design space it seems important to me to stop and discuss the potential drawbacks of locking llama forever and how to address them.

- All Llamas are 1/1, This means some design would become unavailable forever. However this can be an opportunity for extra cash-flow, by allowing peoples to exchange a llama in the protocol for another one for a fee. While for brand perspective floor go up and "strategy" are sexy, this is could be a genuinely useful feature.
- Yield dilution. The more Llamas are locked in the locker the lesser your share of the reward from the monthly distribution. However this effect would not be that big in today's context. Currently 720 llamas are in the locker, add that another 135 are currently in the treasury and thus not lockable (or we revolt), this leave only 256 llamas in the wild, if they were to be all locked this would lead to a maximum of around 26% of dilution.
- The locker, while being quite close to an immutable contract, the distribution of the yield is very much a rug-gable process, should the collection stop the yield distribution or change the contract that get said yield. The protocol would hence need to have a way to wind down or mutate, either automatically, through governance or even just giving the keys to the treasury.

### Design

#### No token

Thanks to the yield from the locker the protocol doesn't NEED a token. By funneling the yield into buying more llamas the protocol can grow it's inventory exponentially. This however would suffer from an absolute zero cold start, needing dozen of years for the yield of one llama to buy a second one, assuming the past yield represent future performance and llama price wouldn't change, and that's still assuming you are starting with 1 llama, while under those assumption a minimum of 10 Llamas would be needed to see an effect on floor price in ones lifespan. This poor offering would also make it hard to generate fee on the side from Llamas exchange. Last nail on the coffin, no token means no presale to pay for stuff like audits or devs.

1. Ask for Llamas as sacrifice
2. lock them
3. use yield to buy more Llamas and goto 2.

#### Copy Paste

The design that would be the closest to the original and with minimal modification would be the one where the yield is used to buy back & burn the protocol token. Incidentally a [protocol doing just that with veAERO NFT](https://x.com/aerostrategyfi) popped in my TL while writting those lines, this is really interesting to see as veAERO are quite close to Llamas in this yield generating NFT property (40 acres for llamas, anynyan ? Imajin auto-repayin' loans on ur llama). 

1. Create a token and put all the liquidity in a token/ETH pool on UNIv4 with a heavy fee
2. As peoples buy the token the protocol who own a huge chunk of the supply of token will start to accrue fee in ETH
3. Those fees are than used to buy a Llama from the collection
4. Lock the Llama
5. When yield is collected, it is used to buy back and burn the token from step 1.

This design stick close to the original and is one of the less complex one except for the no token option. It make the buy-back & burn less sizeable but also less volatile, and more importantly the flywheel doesn't become a liability if for a reason or another the protocol see a long period of inactivity.

#### I fear no lawyer

Buy-back & burn is a meme, it's sole real advantage is in deferring your taxes if your country taxes dividend. But even then wrapper contract are a things but am not your taxes lawyer so whatever. All this to say that instead of buying back the original token and burning it, the yield could be distributed to peoples who staked the token, stakeless can be argued but this way make it easy to not give money to the protocol and doesn't reward peoples providing the liquidity (which is important when your sole source of revenue is trading fee).

1. Create a token and put all the liquidity in a token/ETH pool on UNIv4 with a heavy fee
2. As peoples buy the token the protocol who own a huge chunk of the supply of token will start to accrue fee in ETH
3. Those fees are than used to buy a Llama from the collection
4. Lock the Llama
5. When yield is collected, it is distributed to peoples who staked the token (over the course of a month for MEV reason).

#### Llama Co.

While depending on swap fee is transparent for the user it is a position that will erode over time as peoples will provide liquidity alongside you or even in more attractive pool with smaller swap fee (nb: the protocol would still get swap fee through arbitrage if price moves a lot, but this would be marginal with a 10% fee). The protocol end up in a similar position as the wikimedia foundation, asking for donation, while some peoples will be generous, most of the population will enjoy the ride for free. This misalignment of the players could be problematic in the long run. Instead of relying on swap fee the protocol could directly sell it's token for Llama and redistributing the yields to the token staker closer to a real company. However this approach suffer from a few problems, namely lacking in attractiveness for the investor over buying a Llama directly, the exchange part of the protocol would need to bring a good amount of revenue to make up for it.

1. Exchange a Llama for a fixed price of X token.
2. lock it.
3. distribute the yield to the token staker.

#### Llama strategy

TODO: explain ETH strategy and how it could be translated to llamas

#### The purrfect one

Don't hesitate to share your view.

### Implementation

There are a few point worth mentioning should one want to implement one of the design mentioned earlier.

#### Buying the floor

Most of the strategy do not really check that they are indeed buying the lowest price NFT, they just assume that the market is perfectly efficient and that the pot will grow slowly enough to limit value leak. While those assumption are mostly fine, they still caused issue, especially when no "honest" MEV bot are set up and the TGE rack up a tons of fee. However yield from the locker are definitely not coming in small batch, as such extra precaution needs to be taken, like taking a snapshot of the treasury before collecting the yield and increasing linearly between this value and the one post claim over the course of a few days.

#### One asset to rule them all

The locker can distribute many assets, but it may be interesting to convert them all into a single maybe totally different assets like ETH as it is the one that tends to follow the nft prices the more closely. To do this preliminary research have pointed me to the yearn v3 auction contract. If it is really possible it would simplify the design and even benefit from the infrastructure built around them depending on the circumstances.

#### Upgreadability

As mentioned earlier the Locker contract may only be temporary, as such care need to be taken from the start on how to deal with this possibility. If yield stop what is the plan, how do you detect yield has stopped, many question needs to be answered.

## Conclusion

Game theory can be a fun game, I hope I managed to make your brain cogs turn. Don't hesitate to share your ideal Strategy. The best one get the privilege of having to implement it <2
