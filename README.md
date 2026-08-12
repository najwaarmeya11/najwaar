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
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract FixedOwner {
    address public immutable owner;

    constructor() {
        owner = msg.sender;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract One {
    function get() external pure returns (uint256) {
        return 1;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract ZeroReturner {
    function getZero() external pure returns (uint256) {
        return 0;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract BaseChainId {
    uint256 public constant BASE_CHAIN_ID = 8453;
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract BoolStorage {
    bool public flag;

    function set(bool value) external {
        flag = value;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract EventOnly {
    event Called(address indexed caller);

    function call() external {
        emit Called(msg.sender);
    }// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract PureAdder {
    function add(uint256 x, uint256 y) external pure returns (uint256) {
        return x + y;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract AddressHasher {
    function hash(address addr) external pure returns (bytes32) {
        return keccak256(abi.encodePacked(addr));
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract StringToBytes {
    function toBytes(string calldata text) external pure returns (bytes memory) {
        return bytes(text);
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract BitwiseXor {
    function xor(uint256 a, uint256 b) external pure returns (uint256) {
        return a ^ b;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Bytes32ToUint {
    function convert(bytes32 data) external pure returns (uint256) {
        return uint256(data);
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract StringHash {
    function hash(string calldata text) external pure returns (bytes32) {
        return keccak256(abi.encodePacked(text));
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract TimestampNumber {
    function combine(uint256 number) external view returns (uint256) {
        return block.timestamp + number;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract RevertExample {
    function fail() external pure {
        revert("This always reverts");
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract ReceiveFallback {
    uint256 public receiveCount;
    uint256 public fallbackCount;

    receive() external payable {
        receiveCount++;
    }

    fallback() external {
        fallbackCount++;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract EnumExample {
    enum Status { Pending, Active, Closed }
    Status public status;

    function setActive() external {
        status = Status.Active;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract MemoryExample {
    function process(string memory text) external pure returns (string memory) {
        return text;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

abstract contract AbstractBase {
    function getNumber() public pure virtual returns (uint256);
}

contract Concrete is AbstractBase {
    function getNumber() public pure override returns (uint256) {
        return 100;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract PayableConstructor {
    constructor() payable {}
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract ViewPure {
    uint256 public number = 10;

    function getNumber() external view returns (uint256) {
        return number;
    }

    function add(uint256 a, uint256 b) external pure returns (uint256) {
        return a + b;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

type Price is uint256;

contract CustomType {
    Price public price;

    function setPrice(uint256 value) external {
        price = Price.wrap(value);
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract GasLimit {
    function getGasLimit() external view returns (uint256) {
        return block.gaslimit;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract GasPrice {
    function getGasPrice() external view returns (uint256) {
        return tx.gasprice;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract MsgValueChecker {
    function hasValue() external payable returns (bool) {
        return msg.value > 0;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract CallExample {
    function callContract(address target) external returns (bool) {
        (bool success, ) = target.call("");
        return success;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract BytesConcat {
    function concat(bytes calldata a, bytes calldata b) external pure returns (bytes memory) {
        return bytes.concat(a, b);
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract MemoryArray {
    function create(uint256 size) external pure returns (uint256[] memory) {
        return new uint256[](size);
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract EnumToUint {
    enum State { Off, On, Standby }

    function toUint(State s) external pure returns (uint256) {
        return uint256(s);
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract NamedReturns {
    function get() external pure returns (uint256 number, string memory text) {
        number = 100;
        text = "Hello";
    }
}// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract ForLoop {
    function sum(uint256 n) external pure returns (uint256 total) {
        for (uint256 i = 1; i <= n; i++) {
            total += i;
        }
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract ContinueExample {
    function sumOdd(uint256 n) external pure returns (uint256 total) {
        for (uint256 i = 0; i <= n; i++) {
            if (i % 2 == 0) continue;
            total += i;
        }
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Defaults {
    uint256 public number;      // 0
    bool public flag;           // false
    address public addr;        // address(0)
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract PayableMix {
    function deposit() external payable {}
    function noValue() external pure {}
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract ModifierState {
    uint256 public count;

    modifier increaseCount() {
        count++;
        _;
    }

    function doSomething() external increaseCount {}
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract A {
    function a() public pure returns (string memory) { return "A"; }
}

contract B {
    function b() public pure returns (string memory) { return "B"; }
}

contract C is A, B {}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

library Adder {
    function addOne(uint256 x) internal pure returns (uint256) {
        return x + 1;
    }
}

contract UsingFor {
    using Adder for uint256;

    function test(uint256 x) external pure returns (uint256) {
        return x.addOne();
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract MultiIndexed {
    event Transfer(address indexed from, address indexed to, uint256 indexed amount);

    function transfer(address to, uint256 amount) external {
        emit Transfer(msg.sender, to, amount);
    }
}// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract RequireMessage {
    function check(bool condition) external pure {
        require(condition, "Condition failed");
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract ImmutableGas {
    uint256 public immutable max;

    constructor(uint256 _max) {
        max = _max;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract CalldataLoad {
    function load(uint256 index) external pure returns (uint256 value) {
        assembly {
            value := calldataload(index)
        }
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract CallerAssembly {
    function getCaller() external view returns (address c) {
        assembly {
            c := caller()
        }
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract UintToString {
    function toString(uint256 value) external pure returns (string memory) {
        if (value == 0) return "0";
        uint256 temp = value;
        uint256 digits;
        while (temp != 0) {
            digits++;
            temp /= 10;
        }
        bytes memory buffer = new bytes(digits);
        while (value != 0) {
            digits--;
            buffer[digits] = bytes1(uint8(48 + value % 10));
            value /= 10;
        }
        return string(buffer);
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract IsContractPure {
    function isContract(address addr) external view returns (bool) {
        return addr.code.length > 0;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract ArrayMax {
    function max(uint256[] calldata arr) external pure returns (uint256) {
        require(arr.length > 0, "Empty array");
        uint256 m = arr[0];
        for (uint256 i = 1; i < arr.length; i++) {
            if (arr[i] > m) m = arr[i];
        }
        return m;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract MappingExists {
    mapping(address => uint256) public values;

    function exists(address user) external view returns (bool) {
        return values[user] != 0;
    }

    function set(uint256 value) external {
        values[msg.sender] = value;
    }
}// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract EnumMapping {
    enum Role { None, User, Admin }

    mapping(address => Role) public roles;

    function setRole(Role role) external {
        roles[msg.sender] = role;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract PayableFallback {
    fallback() external payable {}
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract ExactValue {
    function payExact() external payable {
        require(msg.value == 0.01 ether, "Must send exactly 0.01 ETH");
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract PausablePattern {
    bool public paused;
    address public owner = msg.sender;

    modifier whenNotPaused() {
        require(!paused, "Paused");
        _;
    }

    function pause() external {
        require(msg.sender == owner, "Not owner");
        paused = true;
    }

    function unpause() external {
        require(msg.sender == owner, "Not owner");
        paused = false;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract WhitelistPattern {
    mapping(address => bool) public whitelist;
    address public owner = msg.sender;

    function add(address user) external {
        require(msg.sender == owner, "Not owner");
        whitelist[user] = true;
    }

    function isWhitelisted(address user) external view returns (bool) {
        return whitelist[user];
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract SimpleEscrow {
    address public depositor;
    address public beneficiary;
    uint256 public amount;

    function deposit(address _beneficiary) external payable {
        depositor = msg.sender;
        beneficiary = _beneficiary;
        amount = msg.value;
    }

    function release() external {
        require(msg.sender == depositor, "Not depositor");
        payable(beneficiary).transfer(amount);
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract YesNoVote {
    mapping(address => bool) public hasVoted;
    uint256 public yes;
    uint256 public no;

    function vote(bool support) external {
        require(!hasVoted[msg.sender], "Already voted");
        hasVoted[msg.sender] = true;
        if (support) yes++;
        else no++;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract MintCounter {
    uint256 public totalMinted;

    function mint(uint256 amount) external {
        totalMinted += amount;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract TransferEvent {
    event Transfer(address indexed from, address indexed to, uint256 value);

    function fakeTransfer(address to, uint256 value) external {
        emit Transfer(msg.sender, to, value);
    }
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract DomainStyle {
    bytes32 public domainSeparator;

    function setDomain(bytes32 value) external {
        domainSeparator = value;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Deadline {
    function isValid(uint256 deadline) external view returns (bool) {
        return block.timestamp <= deadline;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract PairHash {
    function hash(uint256 a, uint256 b) external pure returns (bytes32) {
        return keccak256(abi.encodePacked(a, b));
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract SaltedHash {
    function hash(bytes32 data, bytes32 salt) external pure returns (bytes32) {
        return keccak256(abi.encodePacked(data, salt));
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract SaltedHash {
    function hash(bytes32 data, bytes32 salt) external pure returns (bytes32) {
        return keccak256(abi.encodePacked(data, salt));
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract SeedGenerator {
    function getSeed() external view returns (bytes32) {
        return keccak256(abi.encodePacked(blockhash(block.number - 1), msg.sender));
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract WinnerChecker {
    uint256 public winningNumber = 42;

    function isWinner(uint256 number) external view returns (bool) {
        return number == winningNumber;
    }
}
