# Polygon-zkEVM

This repository contains instructions and scripts to implement a zk-SNARK circuit using circom, generate a proof, deploy a solidity verifier contract to Sepolia or Mumbai Testnet, and verify the proof.

## Steps to Implement and Verify the zk-SNARK Circuit

### 1. Implement the Circuit

First, write the zk-SNARK circuit in `circuit.circom`. Ensure the circuit correctly represents the functionality you want to prove. Here is a simplified example:

```circom
template Main() {
    signal private input A;
    signal private input B;

    // Constraints and computations here
    A == 0;
    B == 1;
}

component main = Main();
```

### 2. Compile the Circuit

Compile the circom circuit to generate the necessary intermediaries (`wasm`, `json`, `sym`, etc.):

```bash
npx circom circuit.circom -o circuit
```

### 3. Generate a Proof

Generate a proof using the compiled circuit and specific inputs (A=0, B=1):

```bash
npx snarkjs groth16 prove circuit/proving_key.json circuit/proof.json circuit/public.json --witness circuit/witness.json --input circuit/inputs.json
```

### 4. Deploy Solidity Verifier Contract

Deploy a solidity verifier contract to Sepolia or Mumbai Testnet. Ensure the contract includes a `verifyProof` method to verify the generated proof.

### 5. Verify the Proof

Write a script or use Remix IDE to call the `verifyProof` method on the deployed verifier contract. Assert that the output is `true`, confirming the validity of the proof.

### Repository Structure

- **circuit/**: Contains the circom circuit files and generated intermediaries.
- **scripts/**: Optional folder for deployment scripts or verification scripts.
- **README.md**: This file, providing an overview of the project and instructions.

### Dependencies

Ensure you have Node.js and npm installed on your machine. Additionally, install circom and snarkjs:

```bash
npm install -g circom snarkjs
```

## Getting Started

1. Clone this repository.
2. Implement your zk-SNARK circuit in `circuit.circom`.
3. Compile the circuit using `npx circom circuit.circom -o circuit`.
4. Generate a proof using `npx snarkjs groth16 prove circuit/proving_key.json circuit/proof.json circuit/public.json --witness circuit/witness.json --input circuit/inputs.json`.
5. Deploy a solidity verifier contract to Sepolia or Mumbai Testnet.
6. Verify the proof by calling `verifyProof` on the deployed contract and ensuring the output is `true`.

## License

This project is licensed under the MIT License - see the LICENSE file for details.

---

Feel free to adjust the instructions and structure according to your specific implementation details and preferences. This README provides developers with a clear guide to implementing and verifying zk-SNARK circuits using circom and deploying verifier contracts on Sepolia or Mumbai Testnet.
