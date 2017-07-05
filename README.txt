Improving Data Transparency in Clinical Trials Using Blockchain Smart Contracts
===============================================================================

14th May 2017

Authors: Anurag Kumar

Package contents
================

src/Regulator.sol - the solidity smart contract code for the Regulator contract
src/ClinicalTrial.sol - the solidity code smart contract code for the a Clinical Trial contract
src/start-ethereum-node.sh - script to start a local Ethereum node
src/workflow.js - the main nodejs script that interacts with the blockchain
src/run-workflow.sh - script that will execute the workflow steps
src/read-from-blockchain.sh - script that reads trial data from the blockchain
logs/run-workflow.log - output from running src/run-workflow.sh
logs/read-from-blockchain.log - output from running src/read-from-blockchain.sh

Getting started
===============

This code has been tested on OSX 10.12 and Ubuntu 14.04. Code is written using Bash and Javascript - you will need to install nodejs:

https://nodejs.org

sudo apt-get install python-software-properties && curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash - && sudo apt-get install nodejs

We use the testrpc npm module in order to reproduce the exact conditions the workflow scripts need to run the tests. It is important that you reset the blockchain every time you run through these steps. In order to reset, just restart the start-ethereum-node.sh script.

Running the scripts
===================

The steps needed are as follows:

1) Run 'npm install' to install all dependencies mentioned in package.json

2) Install 'testrpc' as a global npm module

npm install -g ethereumjs-testrpc

3) Run the script to start a local Ethereum node

./start-ethereum-node.sh

4) In another terminal, run the script that will execute the workflow steps

./run-workflow.sh > logs/run-workflow.log

This script will:

	-Deploy a Regulator smart contract
	-Add a CRO/pharma to this contract - in this case Roche
	-Upload the trial protocol (data/TrialProtocol.pdf) to IPFS, running locally
	-Deploy a Clinical Trial smart contract - in this case for Tamiflu, including the IPFS hash linking to the protocol
	-Add 500 subjects to the trial
	-Add 5 data points for each subject

5) Run the script to read data from the blockchain contracts
./read-from-blockchain.sh > logs/read-from-blockchain.log