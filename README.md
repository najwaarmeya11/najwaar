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
feat: add owner transfer function to HelloBase

Implemented a transferOwnership function following common patterns. Improves manageability of the contract on Base.
refactor: improve gas efficiency in HelloBase

Optimized storage layout and removed unnecessary operations. Makes the contract cheaper to use on Base.
feat: support multiple greetings in HelloBase

Updated the contract to store and return different greeting messages based on an ID. More versatile for Base experiments.
docs: add Base Sepolia deployment checklist for HelloBase

Created a clear step-by-step checklist for deploying and verifying the contract on Base Sepolia.
feat: make HelloBase greetings updatable by owner only

Restricted the update of greetings to the contract owner. Better access control for Base deployments.
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract HelloBase {
    address public owner;
    mapping(uint256 => string) public greetings;
    uint256 public greetingCount;

    event GreetingAdded(uint256 indexed id, string message);
    event GreetingUpdated(uint256 indexed id, string message);

    modifier onlyOwner() {
        require(msg.sender == owner, "Not owner");
        _;
    }

    constructor() {
        owner = msg.sender;
        greetings[0] = "Hello Base!";
        greetingCount = 1;
    }

    function addGreeting(string calldata message) external onlyOwner {
        greetings[greetingCount] = message;
        emit GreetingAdded(greetingCount, message);
        greetingCount++;
    }

    function updateGreeting(uint256 id, string calldata message) external onlyOwner {
        require(id < greetingCount, "Invalid ID");
        greetings[id] = message;
        emit GreetingUpdated(id, message);
    }

    function getGreeting(uint256 id) external view returns (string memory) {
        require(id < greetingCount, "Invalid ID");
        return greetings[id];
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Greeting {
    string public message = "Hello Base!";

    function setMessage(string calldata _message) external {
        message = _message;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Donation {
    address public owner;
    uint256 public totalDonations;

    constructor() {
        owner = msg.sender;
    }

    function donate() external payable {
        totalDonations += msg.value;
    }

    function withdraw() external {
        require(msg.sender == owner, "Not owner");
        payable(owner).transfer(address(this).balance);
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract OwnershipClaimer {
    address public owner;

    function claim() external {
        require(owner == address(0), "Already claimed");
        owner = msg.sender;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Whitelist {
    address public owner;
    mapping(address => bool) public allowed;

    constructor() {
        owner = msg.sender;
    }

    function add(address user) external {
        require(msg.sender == owner, "Not owner");
        allowed[user] = true;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract IDGenerator {
    uint256 public nextId = 1;

    function getNewId() external returns (uint256) {
        return nextId++;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract UpDownCounter {
    int256 public count;

    function increment() external {
        count++;
    }
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract BoolFlag {
    bool public flag;

    function toggle() external {
        flag = !flag;
    }
}
    function decrement() external {
        count--;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract OpenClose {
    bool public isOpen = true;

    function open() external {
        isOpen = true;
    }

    function close() external {
        isOpen = false;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract HelloWorld {
    string public greet = "Hello Base World!";
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract OwnerGreeter {
    address public owner;
    string public greeting = "gm Base";

    constructor() {
        owner = msg.sender;
    }

    function setGreeting(string calldata _greeting) external {
        require(msg.sender == owner, "Not owner");
        greeting = _greeting;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract MinMax {
    uint256 public min = type(uint256).max;
    uint256 public max;

    function submit(uint256 value) external {
        if (value < min) min = value;
        if (value > max) max = value;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract ZeroChecker {
    function isZero(uint256 number) external pure returns (bool) {
        return number == 0;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract NameStorage {
    string public name;

    function setName(string calldata _name) external {
        name = _name;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract TextHolder {
    string public text = "Base is based";

    function set(string calldata _text) external {
        text = _text;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract TimestampSaver {
    uint256 public savedTime;

    function save() external {
        savedTime = block.timestamp;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Constant {
    function getNumber() external pure returns (uint256) {
        return 42;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract BooleanInverter {
    function invert(bool value) external pure returns (bool) {
        return !value;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract AlwaysTrue {
    function get() external pure returns (bool) {
        return true;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract BytesLength {
    function getLength(bytes calldata data) external pure returns (uint256) {
        return data.length;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract StringComparer {
    function isEqual(string calldata a, string calldata b) external pure returns (bool) {
        return keccak256(abi.encodePacked(a)) == keccak256(abi.encodePacked(b));
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract OwnerChecker {
    address public owner;

    constructor() {
        owner = msg.sender;
    }

    function isOwner() external view returns (bool) {
        return msg.sender == owner;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract AddressEqual {
    function isSame(address a, address b) external pure returns (bool) {
        return a == b;
    }
}// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract MsgValueLogger {
    uint256 public lastValue;

    function log() external payable {
        lastValue = msg.value;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract AddressBalance {
    function getBalance(address addr) external view returns (uint256) {
        return addr.balance;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract EmptyAddress {
    function getZero() external pure returns (address) {
        return address(0);
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract MsgSender {
    function getSender() external view returns (address) {
        return msg.sender;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract TrueConstant {
    bool public constant IS_TRUE = true;
}
