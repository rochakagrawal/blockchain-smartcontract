# blockchain-smartcontract
Smart Contracts written to demonstrate the use of storing documents onto Ethereum Blockchain and tracking their history

This has been submitted for Singapore Blockchain Competion Jan 2023

See supporting files 
Video file - YouTube - link https://youtu.be/eQGaZwBuCcg

Presentation Slides - PDF - https://docs.google.com/presentation/d/1bDbFoJZxv4lqiVpW4Hq7dngd5yn_BPM4Wri0ywABvI4/edit?usp=sharing

Code installation:

1. Please see video link on YouTube for environment needed to run the smart contracts
2. Presentation Slides also has the technology used on Slide 14

Instructions

1. Download the latest public release zip flie
2. Extract the zip file
3. Import the project into Visual Studio Code
4. Install solidity extension / compiiler
5. Install Ganache (auto mining mode)
6. Install Truffle 

Command to run:
1. truffle deploy --network development --reset

> Smart contracts deployed

2. truffle console 

3. Run commands from test.txt inside the test folder 

//Accounts Addresses (derived from Ganache)
A-0: 0xC8804485bb0D5876614Eb0e8B44A3F082C9cbaeD
B-1: 0x3A86DC802BE642BC927ed461Cdd4A62e7884E157
C-2: 0x3b8438f48E7B52056F0080739D09049C30dC59E7
D-3: 0x9E99FE55A48ef57f76827E248165A78aDe2e245f
E-4: 0x43c63AbB3B7c1DC4d7Fcd2CdA657521B1AF512E9
F-5: 0x342857cCfD69cD5a082f6C6685c1FB4D120EE8ad
G-6: 0xD4F01d09EBbc9eE4377F4D5F845CE745935A7550

// Spot check contract has been deployed 
documentJourney.deployed().then(function(instance) {return instance });


// Create 2 issuers  (A,B)  . Issuers can be thought of as candidate hires 
documentJourney.deployed().then(function(instance) {return instance.addEndorser("A","passA","0xC8804485bb0D5876614Eb0e8B44A3F082C9cbaeD","Issuer") });
documentJourney.deployed().then(function(instance) {return instance.addEndorser("B","passB","0x3A86DC802BE642BC927ed461Cdd4A62e7884E157","Issuer") });

//Create 3 endorsers (C, D, E)
documentJourney.deployed().then(function(instance) {return instance.addEndorser("C","passC","0x3b8438f48E7B52056F0080739D09049C30dC59E7","Endorser") });
documentJourney.deployed().then(function(instance) {return instance.addEndorser("D","passD","0x9E99FE55A48ef57f76827E248165A78aDe2e245f","Endorser") });
documentJourney.deployed().then(function(instance) {return instance.addEndorser("E","passE","0x43c63AbB3B7c1DC4d7Fcd2CdA657521B1AF512E9","Endorser") });

// Create 2 validators (F,G)
documentJourney.deployed().then(function(instance) {return instance.addEndorser("F","passF","0x342857cCfD69cD5a082f6C6685c1FB4D120EE8ad","Validator") });
documentJourney.deployed().then(function(instance) {return instance.addEndorser("G","passG","0xD4F01d09EBbc9eE4377F4D5F845CE745935A7550","Validator") });

// Get endorser details  [for testing purposes only]
documentJourney.deployed().then(function(instance) {return instance.getEndorser(0)});
documentJourney.deployed().then(function(instance) {return instance.getEndorser(1)});
documentJourney.deployed().then(function(instance) {return instance.getEndorser(2)});
documentJourney.deployed().then(function(instance) {return instance.getEndorser(3)});
documentJourney.deployed().then(function(instance) {return instance.getEndorser(4)});
documentJourney.deployed().then(function(instance) {return instance.getEndorser(5)});
documentJourney.deployed().then(function(instance) {return instance.getEndorser(6)});

// Create 6 documents all owned by A or B initially
//document[0-2] owned by A (ownerid = 0)
//document [3-5] owned by B (owned id = 1)

// Function specs 
//addDocument(ownerid, documentid, documentype, serial number, cost)

//Execution
documentJourney.deployed().then(function(instance) {return instance.addDocument(0, "Z2377321", "Passport", "123", "0") });
documentJourney.deployed().then(function(instance) {return instance.addDocument(0, "a2339921", "Certificate", "456", 12) });
documentJourney.deployed().then(function(instance) {return instance.addDocument(0, "s84773333", "NRIC", "759", 0, {from: "0xC8804485bb0D5876614Eb0e8B44A3F082C9cbaeD"}) });
documentJourney.deployed().then(function(instance) {return instance.addDocument(1, "A1233333", "Passport", "789", 0, {from: "0x3A86DC802BE642BC927ed461Cdd4A62e7884E157"}) });
documentJourney.deployed().then(function(instance) {return instance.addDocument(1, "2321321", "Certificate", "135", 14, {from: "0x3A86DC802BE642BC927ed461Cdd4A62e7884E157"}) });
documentJourney.deployed().then(function(instance) {return instance.addDocument(1, "t20327221", "Citizenship", "357", 60, {from: "0x3A86DC802BE642BC927ed461Cdd4A62e7884E157"}) });


// Get document details [for testing purposes only]
documentJourney.deployed().then(function(instance) {return instance.getDocument(0) });
documentJourney.deployed().then(function(instance) {return instance.getDocument(1) });
documentJourney.deployed().then(function(instance) {return instance.getDocument(2) });
documentJourney.deployed().then(function(instance) {return instance.getDocument(3) });
documentJourney.deployed().then(function(instance) {return instance.getDocument(4) });
documentJourney.deployed().then(function(instance) {return instance.getDocument(5) });

// Move products along Endorsement / Background verification chain: Issuer=> Endorser=> Endorser=> Validator
//function newOwner(uint user1_id ,uint user2_id, uint prod_id) onlyOwner(prod_id) public returns(bool)
// A=0, B=1, C=2, D=3, E=4, F=5, G=6

//A sending to C for endorsement. Document [0] . Passport 
documentJourney.deployed().then(function(instance) {return instance.newOwner(0, 2, 0, {from: "0xC8804485bb0D5876614Eb0e8B44A3F082C9cbaeD"}) });

//A sending to D for endorsement. Document [1] .  Certificate
documentJourney.deployed().then(function(instance) {return instance.newOwner(0, 3, 1, {from: "0xC8804485bb0D5876614Eb0e8B44A3F082C9cbaeD"}) });

// A sending to E for endorsement. Document [2] .   NRIC
documentJourney.deployed().then(function(instance) {return instance.newOwner(0, 4, 2, {from: "0xC8804485bb0D5876614Eb0e8B44A3F082C9cbaeD"}) });

// B sending to E for endorsement. Document [3] .  Passport 
documentJourney.deployed().then(function(instance) {return instance.newOwner(1, 4, 3, {from: "0x3A86DC802BE642BC927ed461Cdd4A62e7884E157"}) });

// C sending to E for endorsement. Document [0] . Passport 
documentJourney.deployed().then(function(instance) {return instance.newOwner(2, 4, 0, {from: "0x3b8438f48E7B52056F0080739D09049C30dC59E7"}) });

// E sending to G for validation. Document [0].     Passport 
documentJourney.deployed().then(function(instance) {return instance.newOwner(4, 6, 0, {from: "0x43c63AbB3B7c1DC4d7Fcd2CdA657521B1AF512E9"}) });

//check who is the owner right now 
documentJourney.deployed().then(function(instance) {return instance.getCurrentOwnership(0) });

//get track by document ID 
documentJourney.deployed().then(function(instance) {return instance.getProvenance(0) });
documentJourney.deployed().then(function(instance) {return instance.getProvenance(1) });
documentJourney.deployed().then(function(instance) {return instance.getProvenance(2) });
documentJourney.deployed().then(function(instance) {return instance.getProvenance(3) });
documentJourney.deployed().then(function(instance) {return instance.getProvenance(4) });
documentJourney.deployed().then(function(instance) {return instance.getProvenance(5) });

//get credibility score
documentJourney.deployed().then(function(instance) {return instance.getCredibilityScore(0) });

--

//check total coin supply 
credibilityToken.deployed().then(function(instance) {return instance.totSupply() });

// Show  balance of A and B
credibilityToken.deployed().then(function(instance) {return instance.balanceOf("0xC8804485bb0D5876614Eb0e8B44A3F082C9cbaeD") });
credibilityToken.deployed().then(function(instance) {return instance.balanceOf("0x3A86DC802BE642BC927ed461Cdd4A62e7884E157") });

//initially A has all tokens 
credibilityToken.deployed().then(function(instance) {return instance.balanceOf("0xC8804485bb0D5876614Eb0e8B44A3F082C9cbaeD") });

// B is approved for 10000 tokens 
credibilityToken.deployed().then(function(instance) {return instance.approve("0x3A86DC802BE642BC927ed461Cdd4A62e7884E157",10000) });

// A is tranferring 100 token to B
credibilityToken.deployed().then(function(instance) {return instance.transferFrom("0xC8804485bb0D5876614Eb0e8B44A3F082C9cbaeD","0x3A86DC802BE642BC927ed461Cdd4A62e7884E157",100) });

// Show updated balance of A and B
credibilityToken.deployed().then(function(instance) {return instance.balanceOf("0xC8804485bb0D5876614Eb0e8B44A3F082C9cbaeD") });
credibilityToken.deployed().then(function(instance) {return instance.balanceOf("0x3A86DC802BE642BC927ed461Cdd4A62e7884E157") });




