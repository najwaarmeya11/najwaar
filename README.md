Setting up the foundation for learning and building on Base. Excited to explore smart contracts, tooling and the growing onchain economy on this L2.
docs: explain gas savings and developer experience on Base

Compared to Ethereum mainnet, Base offers significantly lower fees while keeping full EVM compatibility. This commit expands the README with practical notes for builders joining the Base Guild.
feat: create HelloBase contract

New HelloBase.sol that returns a greeting message. Minimal contract to practice deployment and interaction on the Base network.
feat: update HelloBase with customizable greeting

Modified the contract to allow setting a custom greeting message. Makes it more flexible for testing on Base.
feat: make HelloBase greeting persistent

Stored the greeting in a state variable so it persists between calls. Ready for real interactions on Base Sepolia.
docs: update README with HelloBase usage examples

Added clear examples of how to call the greeting functions after deploying on Base Sepolia or Mainnet.
