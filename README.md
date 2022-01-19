# hello-zk
zk snark demo
https://docs.circom.io/getting-started

### build
* circom src/01-hello.circom --r1cs --wasm --sym --c -o build/01
* node generate_witness.js hello.wasm ../input.json ../witness.wtns
* make
* snarkjs powersoftau new bn128 12 pot12_0000.ptau -v
* snarkjs powersoftau contribute pot12_0000.ptau pot12_0001.ptau --name="First contribution" -v
  > hi
* snarkjs powersoftau prepare phase2 pot12_0001.ptau pot12_final.ptau -v
* snarkjs groth16 setup hello.r1cs pot12_final.ptau hello_0000.zkey
* snarkjs zkey contribute hello_0000.zkey hello_0001.zkey --name="1st Contributor Name" -v
  > hii
* snarkjs zkey export verificationkey hello_0001.zkey verification_key.json
* snarkjs groth16 prove hello_0001.zkey witness.wtns proof.json public.json
* snarkjs groth16 verify verification_key.json public.json proof.json
* snarkjs zkey export solidityverifier hello_0001.zkey verifier.sol