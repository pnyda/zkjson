# zkJSON
JSON parser written in Lurk

# Description
Let's say there's Alice and Bob. Both know a poseidon hash $H$, a path $P$, and a value $V$. Only Alice knows the preimage of $H$ called $J$. zkJSON lets Alice prove to Bob without disclosing $J$ that

- $J$ is a valid JSON.
- $J$ contains $V$ under the path $P$.

# Usage
Copy and paste [put-it-all-together.lurk](put-it-all-together.lurk) into [clutch](https://github.com/lurk-lab/lurk-rs/tree/master/clutch). Currently this repository needs [a patch for Lurk](https://github.com/lurk-lab/lurk-rs/pull/432) to work.

# TODO
## Make it faster
Currently the proof verification can be done in seconds. But the proof generation takes hours. Possible optimizations might be:

- Hide only values. Make keys of an object public. This approach makes the proving significantly faster at the expense of privacy, according to [Chainlink Blog](https://blog.chain.link/deco-parsing-the-response/).
- [simdjson](https://github.com/simdjson/simdjson) style parallelization. This approach needs Lurk to support parallel proving upstream.

## Write tests
I need a better testing framework for Lurk.

## Better interface
CLI command to generate a proof / verify a proof would be nice.

## Secure cryptography
According to an audit, the commitment scheme used in Nova, a dependency of Lurk, is not completely hiding. I'm no cryptography expert but I guess we can't use this repository in production until [this issue](https://github.com/microsoft/Nova/issues/174) gets resolved.
