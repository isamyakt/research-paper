# Graph Protocol Supports Solana with Substreams

## 1. Substreams

    - By using the new substreams technology, developers can efficiently extract and interpret on-chain data from Solana’s mainnet-beta to feed their applications. 
      Providing support with substreams is the first step in bringing subgraphs to Solana.
      
    - Developers can use substreams modules, coded in Rust, to build protocol-specific data streams or market-wide analytical datasets. 
      They can also be used to power real-time notifications, and display long, time-series information. 
      
    - Substreams open the door to many benefits, including: feeding any data systems through technology-specific sinks, reusing your Solana program’s Rust code to 
      read on-chain data, a laser-focused debugging experience, communal and composable refinement of data streams, and reliable reorg-aware streams.
      
    - substreams are poised to unlock subgraph performance with parallel data processing to greatly increase syncing speeds. Through a horizontally scalable parallel engine, 
      substreams are capable of multiplying historical indexing performance by more than 100x.
      
    - Developers can utilize substreams to generate new and exciting use cases, such as cross-chain bridges, large-scale analytics, refined intelligence for block explorers, 
      trading engines, and any application in need of a rich, consistent data stream.
    
### How does Substreams Work?

1. RPC-based Subgraphs have a linear indexing model for processing blockchain data (i.e. they process events one at a time, in order). They do so via polling API calls to Solana clients. Firehose technology replaces those polling API calls with a stream of data utilizing a push model and sending data to the indexing node faster. This helps increase the speed of syncing and indexing.

2. Substreams take things even further by enabling massively parallelized streaming data. Substreams can be combined and aggregated in powerful new ways to feed data into subgraphs or end-user applications in a fraction of the time. With substream parallelization, some subgraphs could sync more than 100x faster.

3. With substreams, the data pipeline can be broken down into four stages:

    - Extract (via Firehose)
    - Transform (via Substreams and Subgraphs)
    - Load (to the postgres database)
    - Query (serving queries to users)
    - The first transformation via substreams allows lighter weight parallelized computation and composability that many subgraphs can benefit from.

4. To illustrate: in the instance of large DEXes—which need to find pairs for any given trade—a substream model enables individual small modules to work simultaneously on pairs, reserve extractors, prices, volume aggregation, and other key metrics. If a developer bases their work on existing substreams, they can take the DEX prices and create a module to average all DEX prices across an ecosystem.

5. Substream modules don’t go through postgresQL. Existing modules can be leveraged, which developers can adapt, allowing end users to take advantage of composability without paying a performance penalty for indexing.

6. After the Extraction and Transformation stages, substreams can be composed in an infinite number of ways, enabling another module to populate into a subgraph, all before Load operations.

7. As opposed to linear historical data processing, substream data can be processed in parallel and cached. This allows for the fastest possible insertion into the postgres database, going from days or weeks to mere hours.

8. This all serves as a benefit to developers. Developers need to build subgraphs and should be able to iterate on those subgraphs as fast as possible, maximizing developer productivity. Developers will be able to iterate upon existing modules, reuse the most efficient processes (such as in the DEX example), using incremental iterations to improve without needing to rebuild a new subgraph. They will be able to observe data and add to their database as required. The speed and data composability of subgraphs and substreams, pulling data through Firehose, will make The Graph the fastest and most efficient way to get data from blockchains.

9. This is the power of open-source data composability via The Graph: a hivemind of developers building composable data across a global ecosystem. Centralized services cannot compete.

### Features of Substreams

* Substreams are new data sources on The Graph Protocol that more efficiently extract enriched data through modules built in Rust. While substreams can be used independently, there are ongoing efforts to integrate substreams to power subgraphs and be supported on The Graph Network.

* Substreams were created by StreamingFast, a core devs that has worked across many chains to learn the needs for data-indexing architecture. Following the launch of Firehose, which revealed the potential efficiencies of extracting data to optimize indexing, substreams were created to unlock greater opportunities for dapp developers.

* In an ETL (extract, transform, load) analogy, substreams are the transformation layer, whereas Firehose is the extraction layer. By contrast, subgraphs provide the full ETLQ experience, including the load and query layers.

* RPC-based indexing technologies usually poll API from the native chain clients. Firehose technology replaces those polling API calls with a stream of data utilizing a push model and sending data to the indexing node faster. This increases the speed of syncing and indexing, and does away with most needs for archive nodes.

* Substreams, which are blockchain agnostic, take things even further by enabling massively parallelized streaming data. Substreams can be combined in powerful new ways to feed data into subgraphs or end-user applications in a fraction of the time. Early testing on some subgraphs saw sync speed increases of over 100x with substreams parallelization.

* Because substreams support stateful modules, analytic use cases can aggregate computations across the history of the chain, even in parallel, enabling new powerful ad-hoc analysis to be performed.

* Substreams can feed into many sinks, with Postgres and MongoDB already available, and graph-node integration on its way. Substreams can also easily be consumed by simple programs written in any language that supports gRPC (Python, Go, Rust, C/#/++, Java/Kotlin and more), feeding into any system you may already have.

* With any Solana programs being written in Rust, instructions can be decoded in substreams using the same code you use to validate transactions on-chain, targeting WebAssembly instead of BPF.

* Being fully deterministic, substreams have excellent caching capabilities. They allow you to leverage the cached state of previously executed modules to jump in the middle of history to zero in on a bug without starting over from the beginning. Once dependencies of your module have been processed once, anyone can start building off of it, at any point in time in on-chain history. This massively impacts agility and speed of iteration.

* Substreams also create new forms of in-flight composition. This means that modules taken from different authors can be combined together at the time of transformation, not at a later query time.

* As an example, substreams make it possible to use a Open Book Dex price module developed by team A, combine it with a Metaplex sales module developed by team B, and then create a third, enriched and refined USD volume of trades, developed by yourself. Each stream would stay independently composable. So, if you need to access data on prices, you could just hook into the prices module; or if you need sales volumes, you could just hook into the sales volume module.

* Lastly, reliability is baked into the substream technology in the form of a cursor, accompanying every streamed payload. This cursor can be sent back in the next request in case of disconnection - just like a web cookie - and guarantees that you will never miss any re-org signal, even if the event happened while you were disconnected.

* According to graph protocol, full-fledged integration of substreams across chains as well as a subgraph-substreams integration to bring performance improvements to subgraphs is coming soon. When combining the speed and data composability of subgraphs and substreams with unpacked blockchain data from the Firehose, The Graph is unarguably the fastest and most efficient way to get data from blockchains.

- [x] Addional Resources
    - StreamingFast [link](https://www.streamingfast.io/)
    - Substreams developer [guide](https://substreams.streamingfast.io/developer-guide)
    - Substreams [docs](https://substreams.streamingfast.io/)
    - Substreams [github](https://github.com/streamingfast/substreams-rs)
    - Chains & Endpoints [docs](https://substreams.streamingfast.io/reference-and-specs/chains-and-endpoints)
    - Substreams [Discord](https://discord.gg/jZwqxJAvRs)
    - Firehose [docs](https://firehose.streamingfast.io/)

