Tools to generate and verify Merkle Paths for a set of files.

This tool is useful to generate a record in Hathor mainnet so that an external auditor can verify that no files have been changed. It also ensure that these files existed at the time they were stored at the blockchain.

The common use for this tool is the following:

1. Generate the files that will be auditable.
2. Build the merkle paths.
3. Store the merkle root in Hathor mainnet.
4. Share any subset of files with an external auditor, so they can verify the files existed and were not changed.

## How to use?

To generate merkle paths, run `./merkle-tree build output file [file ...]`.

To verify a file, run `./merkle-tree verify csvfile file [file ...]`.

The `csvfile` in the verify command must be the `output` generated by the build command (see the example below). You can run `./merkle-tree --help` to get additional help.

When sharing with an external auditor, the csv file can be safely filtered to include only the files the auditor will have access. For clarity, you can either share the whole csv file or just the lines of the files to be audited.

Here is an example with random data:

```bash
# Generate random files
mkdir ./data
for f in a{0..9} b{0..9} c{0..9}; do echo $RANDOM > ./data/$f; done

# Generate merkle path for all files
./merkle-tree build paths.csv data/*

# Verify merkle paths for all files starting with b
./merkle-tree verify paths.csv data/b*
```

Here is the output. Note that the merkle root is the value that must be stored in Hathor mainnet.

```
> ./merkle-tree build paths.csv data/*
paths.csv successfully generated with 30 files.
merkle root: 2e47bf1834c0e6a5a5d4ddc191924a3bbbb28db6add43d206823d81371601934

> ./merkle-tree verify paths.csv data/b*
data/b0: success
data/b1: success
data/b2: success
data/b3: success
data/b4: success
data/b5: success
data/b6: success
data/b7: success
data/b8: success
data/b9: success
```

Here is the content of the `paths.csv` generated on the example above. Note that you will get different results on your computer since the files have random numbers.

```csv
filename,file_hash_method,file_hash,merkle_tree_hash_method,root_hash,merkle_path
data/a0,md5,864837b4982abc5e7f2d436ee63fa9ea,sha256,2e47bf1834c0e6a5a5d4ddc191924a3bbbb28db6add43d206823d81371601934,R:6b59a2966967da8358d43e9fa003c42d R:aa5aac588cd214b2a329050f4c96268061239ec82bb67bfe11a07792d590b548 R:634f4ded9e005c81daad4e8c34f3dd4c9618dbdd35ea1d725a255d1fc0d329b4 R:9af80b43501db678b4affebbb5e897633f7b880d175febf8a4fd6eed60c3028e R:aa481092f48b226bb1e93b4e44a2afd0fb20448ce9c59f4979932d30d9d0257c
data/a1,md5,6b59a2966967da8358d43e9fa003c42d,sha256,2e47bf1834c0e6a5a5d4ddc191924a3bbbb28db6add43d206823d81371601934,L:864837b4982abc5e7f2d436ee63fa9ea R:aa5aac588cd214b2a329050f4c96268061239ec82bb67bfe11a07792d590b548 R:634f4ded9e005c81daad4e8c34f3dd4c9618dbdd35ea1d725a255d1fc0d329b4 R:9af80b43501db678b4affebbb5e897633f7b880d175febf8a4fd6eed60c3028e R:aa481092f48b226bb1e93b4e44a2afd0fb20448ce9c59f4979932d30d9d0257c
data/a2,md5,d95834eeab7316c7f52a14f5ae2839b6,sha256,2e47bf1834c0e6a5a5d4ddc191924a3bbbb28db6add43d206823d81371601934,R:94f7d5a6fd009b47ebcc6deb3c499d19 L:f6511353962176b7a7723b60b6c443b0204f45517fd0337fc624e3f1343522f8 R:634f4ded9e005c81daad4e8c34f3dd4c9618dbdd35ea1d725a255d1fc0d329b4 R:9af80b43501db678b4affebbb5e897633f7b880d175febf8a4fd6eed60c3028e R:aa481092f48b226bb1e93b4e44a2afd0fb20448ce9c59f4979932d30d9d0257c
data/a3,md5,94f7d5a6fd009b47ebcc6deb3c499d19,sha256,2e47bf1834c0e6a5a5d4ddc191924a3bbbb28db6add43d206823d81371601934,L:d95834eeab7316c7f52a14f5ae2839b6 L:f6511353962176b7a7723b60b6c443b0204f45517fd0337fc624e3f1343522f8 R:634f4ded9e005c81daad4e8c34f3dd4c9618dbdd35ea1d725a255d1fc0d329b4 R:9af80b43501db678b4affebbb5e897633f7b880d175febf8a4fd6eed60c3028e R:aa481092f48b226bb1e93b4e44a2afd0fb20448ce9c59f4979932d30d9d0257c
data/a4,md5,8018fd80c242093bafa1d485b1447b42,sha256,2e47bf1834c0e6a5a5d4ddc191924a3bbbb28db6add43d206823d81371601934,R:04a483774359b6ab5b09dc1f05883fb5 R:f2df960a3cf9627b847c999a1c881bfb835eb9f240bb37c4fd9435beffe62bc1 L:44d752e03db1bc9b1707990eb0c4d43fb5160663a7dede7c777adde31126dd5f R:9af80b43501db678b4affebbb5e897633f7b880d175febf8a4fd6eed60c3028e R:aa481092f48b226bb1e93b4e44a2afd0fb20448ce9c59f4979932d30d9d0257c
data/a5,md5,04a483774359b6ab5b09dc1f05883fb5,sha256,2e47bf1834c0e6a5a5d4ddc191924a3bbbb28db6add43d206823d81371601934,L:8018fd80c242093bafa1d485b1447b42 R:f2df960a3cf9627b847c999a1c881bfb835eb9f240bb37c4fd9435beffe62bc1 L:44d752e03db1bc9b1707990eb0c4d43fb5160663a7dede7c777adde31126dd5f R:9af80b43501db678b4affebbb5e897633f7b880d175febf8a4fd6eed60c3028e R:aa481092f48b226bb1e93b4e44a2afd0fb20448ce9c59f4979932d30d9d0257c
data/a6,md5,2213eeaf73de37be80390ce3d261f2ac,sha256,2e47bf1834c0e6a5a5d4ddc191924a3bbbb28db6add43d206823d81371601934,R:03002b8f9992fc4e2c80672260de435f L:8d5e9f933e40ba624dc0981dbe74b80b180a21ad9e6220bea22d07de117c0599 L:44d752e03db1bc9b1707990eb0c4d43fb5160663a7dede7c777adde31126dd5f R:9af80b43501db678b4affebbb5e897633f7b880d175febf8a4fd6eed60c3028e R:aa481092f48b226bb1e93b4e44a2afd0fb20448ce9c59f4979932d30d9d0257c
data/a7,md5,03002b8f9992fc4e2c80672260de435f,sha256,2e47bf1834c0e6a5a5d4ddc191924a3bbbb28db6add43d206823d81371601934,L:2213eeaf73de37be80390ce3d261f2ac L:8d5e9f933e40ba624dc0981dbe74b80b180a21ad9e6220bea22d07de117c0599 L:44d752e03db1bc9b1707990eb0c4d43fb5160663a7dede7c777adde31126dd5f R:9af80b43501db678b4affebbb5e897633f7b880d175febf8a4fd6eed60c3028e R:aa481092f48b226bb1e93b4e44a2afd0fb20448ce9c59f4979932d30d9d0257c
data/a8,md5,978007cdab3a549537f5930a616c49c0,sha256,2e47bf1834c0e6a5a5d4ddc191924a3bbbb28db6add43d206823d81371601934,R:8cc744e9dbe90a3f796126c4429a71e4 R:96d68d25344d994d6b565446b3bb4ec94e7795299eb50d669153af860fd563f4 R:18660823e3200ebd4396a5c1cb3bfa0241f32ee00144398d71fe718f2e322a47 L:4eb005fde8fbdcf3ad233c94540a36a4b91425e785b504bd24031207ee844d94 R:aa481092f48b226bb1e93b4e44a2afd0fb20448ce9c59f4979932d30d9d0257c
data/a9,md5,8cc744e9dbe90a3f796126c4429a71e4,sha256,2e47bf1834c0e6a5a5d4ddc191924a3bbbb28db6add43d206823d81371601934,L:978007cdab3a549537f5930a616c49c0 R:96d68d25344d994d6b565446b3bb4ec94e7795299eb50d669153af860fd563f4 R:18660823e3200ebd4396a5c1cb3bfa0241f32ee00144398d71fe718f2e322a47 L:4eb005fde8fbdcf3ad233c94540a36a4b91425e785b504bd24031207ee844d94 R:aa481092f48b226bb1e93b4e44a2afd0fb20448ce9c59f4979932d30d9d0257c
data/b0,md5,f337746ae1587ca821ace3bfdcf26d1e,sha256,2e47bf1834c0e6a5a5d4ddc191924a3bbbb28db6add43d206823d81371601934,R:e2b1da7ecbe54f7a395a3ee689524aa4 L:083ccd687cf1232c0eb6cbbe286c9e4031a166c0f5a50cf76e788d24a4857f84 R:18660823e3200ebd4396a5c1cb3bfa0241f32ee00144398d71fe718f2e322a47 L:4eb005fde8fbdcf3ad233c94540a36a4b91425e785b504bd24031207ee844d94 R:aa481092f48b226bb1e93b4e44a2afd0fb20448ce9c59f4979932d30d9d0257c
data/b1,md5,e2b1da7ecbe54f7a395a3ee689524aa4,sha256,2e47bf1834c0e6a5a5d4ddc191924a3bbbb28db6add43d206823d81371601934,L:f337746ae1587ca821ace3bfdcf26d1e L:083ccd687cf1232c0eb6cbbe286c9e4031a166c0f5a50cf76e788d24a4857f84 R:18660823e3200ebd4396a5c1cb3bfa0241f32ee00144398d71fe718f2e322a47 L:4eb005fde8fbdcf3ad233c94540a36a4b91425e785b504bd24031207ee844d94 R:aa481092f48b226bb1e93b4e44a2afd0fb20448ce9c59f4979932d30d9d0257c
data/b2,md5,159a772080de66ba7d7be9143f598a5c,sha256,2e47bf1834c0e6a5a5d4ddc191924a3bbbb28db6add43d206823d81371601934,R:512bd03ef99b2cb170926cd7435e6c0c R:585a771443b8c03338e8e09f4b0315a4a3d2ca350403528cd70a033c1af5272a L:7a103c57b21c431d229cdaa4797e4577638067aab53fb2d15c67acb70aa778a0 L:4eb005fde8fbdcf3ad233c94540a36a4b91425e785b504bd24031207ee844d94 R:aa481092f48b226bb1e93b4e44a2afd0fb20448ce9c59f4979932d30d9d0257c
data/b3,md5,512bd03ef99b2cb170926cd7435e6c0c,sha256,2e47bf1834c0e6a5a5d4ddc191924a3bbbb28db6add43d206823d81371601934,L:159a772080de66ba7d7be9143f598a5c R:585a771443b8c03338e8e09f4b0315a4a3d2ca350403528cd70a033c1af5272a L:7a103c57b21c431d229cdaa4797e4577638067aab53fb2d15c67acb70aa778a0 L:4eb005fde8fbdcf3ad233c94540a36a4b91425e785b504bd24031207ee844d94 R:aa481092f48b226bb1e93b4e44a2afd0fb20448ce9c59f4979932d30d9d0257c
data/b4,md5,bdab2571af45ed863c3ce7d2d0e6bca1,sha256,2e47bf1834c0e6a5a5d4ddc191924a3bbbb28db6add43d206823d81371601934,R:833a081ae933dbce059f4cbeef21a722 L:b926a049031d17e99809e30f5a4e7ea663c3b2b99cd3b52a07a9b117fe9701cc L:7a103c57b21c431d229cdaa4797e4577638067aab53fb2d15c67acb70aa778a0 L:4eb005fde8fbdcf3ad233c94540a36a4b91425e785b504bd24031207ee844d94 R:aa481092f48b226bb1e93b4e44a2afd0fb20448ce9c59f4979932d30d9d0257c
data/b5,md5,833a081ae933dbce059f4cbeef21a722,sha256,2e47bf1834c0e6a5a5d4ddc191924a3bbbb28db6add43d206823d81371601934,L:bdab2571af45ed863c3ce7d2d0e6bca1 L:b926a049031d17e99809e30f5a4e7ea663c3b2b99cd3b52a07a9b117fe9701cc L:7a103c57b21c431d229cdaa4797e4577638067aab53fb2d15c67acb70aa778a0 L:4eb005fde8fbdcf3ad233c94540a36a4b91425e785b504bd24031207ee844d94 R:aa481092f48b226bb1e93b4e44a2afd0fb20448ce9c59f4979932d30d9d0257c
data/b6,md5,014670f1df1afa386f2f1be56e421a5d,sha256,2e47bf1834c0e6a5a5d4ddc191924a3bbbb28db6add43d206823d81371601934,R:7845f8e7225091c7c96c5a8a102ca5b5 R:16cfe266e6f4b216ffa70fd98f9d439c803683fbe3ec2d917c257f6896ec94d0 R:a134afdfceb30fe45ceae5038d54e7779e456c776dcdb73be73de38004527a07 R:625231abf452d906841c4d0532c860669fd0d60ab8776baa4688613978f509c4 L:7b5feb4c4ebafd8cae1e786de58f8f98e2cf59417ca6632bc6b17ed99c2d8184
data/b7,md5,7845f8e7225091c7c96c5a8a102ca5b5,sha256,2e47bf1834c0e6a5a5d4ddc191924a3bbbb28db6add43d206823d81371601934,L:014670f1df1afa386f2f1be56e421a5d R:16cfe266e6f4b216ffa70fd98f9d439c803683fbe3ec2d917c257f6896ec94d0 R:a134afdfceb30fe45ceae5038d54e7779e456c776dcdb73be73de38004527a07 R:625231abf452d906841c4d0532c860669fd0d60ab8776baa4688613978f509c4 L:7b5feb4c4ebafd8cae1e786de58f8f98e2cf59417ca6632bc6b17ed99c2d8184
data/b8,md5,271b8d91670aced1ea7a91141804c53c,sha256,2e47bf1834c0e6a5a5d4ddc191924a3bbbb28db6add43d206823d81371601934,R:769fbcdd78085ef434acf48020c25c7e L:43b3bfc0c5ea2f144339f5794d7e15ea4d4003ac2fe9e6597421d380adc13990 R:a134afdfceb30fe45ceae5038d54e7779e456c776dcdb73be73de38004527a07 R:625231abf452d906841c4d0532c860669fd0d60ab8776baa4688613978f509c4 L:7b5feb4c4ebafd8cae1e786de58f8f98e2cf59417ca6632bc6b17ed99c2d8184
data/b9,md5,769fbcdd78085ef434acf48020c25c7e,sha256,2e47bf1834c0e6a5a5d4ddc191924a3bbbb28db6add43d206823d81371601934,L:271b8d91670aced1ea7a91141804c53c L:43b3bfc0c5ea2f144339f5794d7e15ea4d4003ac2fe9e6597421d380adc13990 R:a134afdfceb30fe45ceae5038d54e7779e456c776dcdb73be73de38004527a07 R:625231abf452d906841c4d0532c860669fd0d60ab8776baa4688613978f509c4 L:7b5feb4c4ebafd8cae1e786de58f8f98e2cf59417ca6632bc6b17ed99c2d8184
data/c0,md5,c6bafa26ba7f51c3734b2b02b3edd2bb,sha256,2e47bf1834c0e6a5a5d4ddc191924a3bbbb28db6add43d206823d81371601934,R:4f25462d961554add32ea87d3b0f1b3b R:e862a1dfb9bf9e726901ee828e2f9f9efa59f66039674dd6e9e241552fa6f01e L:ada80cf82d2d70dd0f8c35f2d84cf72298422b5a2f741670f9911c513ae51869 R:625231abf452d906841c4d0532c860669fd0d60ab8776baa4688613978f509c4 L:7b5feb4c4ebafd8cae1e786de58f8f98e2cf59417ca6632bc6b17ed99c2d8184
data/c1,md5,4f25462d961554add32ea87d3b0f1b3b,sha256,2e47bf1834c0e6a5a5d4ddc191924a3bbbb28db6add43d206823d81371601934,L:c6bafa26ba7f51c3734b2b02b3edd2bb R:e862a1dfb9bf9e726901ee828e2f9f9efa59f66039674dd6e9e241552fa6f01e L:ada80cf82d2d70dd0f8c35f2d84cf72298422b5a2f741670f9911c513ae51869 R:625231abf452d906841c4d0532c860669fd0d60ab8776baa4688613978f509c4 L:7b5feb4c4ebafd8cae1e786de58f8f98e2cf59417ca6632bc6b17ed99c2d8184
data/c2,md5,72388db9c6f10c5f9c994d605c691365,sha256,2e47bf1834c0e6a5a5d4ddc191924a3bbbb28db6add43d206823d81371601934,R:4fa68093d6a243fe993cc8769933aa9b L:d33bd1c1e97ad1e735c6691482e754d9054607f87038a3c2363af79e16c7b881 L:ada80cf82d2d70dd0f8c35f2d84cf72298422b5a2f741670f9911c513ae51869 R:625231abf452d906841c4d0532c860669fd0d60ab8776baa4688613978f509c4 L:7b5feb4c4ebafd8cae1e786de58f8f98e2cf59417ca6632bc6b17ed99c2d8184
data/c3,md5,4fa68093d6a243fe993cc8769933aa9b,sha256,2e47bf1834c0e6a5a5d4ddc191924a3bbbb28db6add43d206823d81371601934,L:72388db9c6f10c5f9c994d605c691365 L:d33bd1c1e97ad1e735c6691482e754d9054607f87038a3c2363af79e16c7b881 L:ada80cf82d2d70dd0f8c35f2d84cf72298422b5a2f741670f9911c513ae51869 R:625231abf452d906841c4d0532c860669fd0d60ab8776baa4688613978f509c4 L:7b5feb4c4ebafd8cae1e786de58f8f98e2cf59417ca6632bc6b17ed99c2d8184
data/c4,md5,308e02a6acd4230d1502a842099590d6,sha256,2e47bf1834c0e6a5a5d4ddc191924a3bbbb28db6add43d206823d81371601934,R:dd7e54d794396e03549cc3c05a0ea6f1 R:4a3062ec5569655cb1e50f58efcc2b00a85fc29b96fa3cf1f5f8775619e68cef R:fd0feb0200c97b79e3333b45c0136420fcc953d9e5206d500d4d47ce96d6be96 L:05a3a85ac8ccfd1b24329c049483580dcecb30dd24d208b9470c031e1e208341 L:7b5feb4c4ebafd8cae1e786de58f8f98e2cf59417ca6632bc6b17ed99c2d8184
data/c5,md5,dd7e54d794396e03549cc3c05a0ea6f1,sha256,2e47bf1834c0e6a5a5d4ddc191924a3bbbb28db6add43d206823d81371601934,L:308e02a6acd4230d1502a842099590d6 R:4a3062ec5569655cb1e50f58efcc2b00a85fc29b96fa3cf1f5f8775619e68cef R:fd0feb0200c97b79e3333b45c0136420fcc953d9e5206d500d4d47ce96d6be96 L:05a3a85ac8ccfd1b24329c049483580dcecb30dd24d208b9470c031e1e208341 L:7b5feb4c4ebafd8cae1e786de58f8f98e2cf59417ca6632bc6b17ed99c2d8184
data/c6,md5,0f4a54d8d5678b878e6c05dc38e64d5f,sha256,2e47bf1834c0e6a5a5d4ddc191924a3bbbb28db6add43d206823d81371601934,R:b4b5b6ad198fe121905d0779b24414e6 L:73093d69d6202d0ba24ae3ee5fb011d695f550a5e506efcbcef48f61039e983c R:fd0feb0200c97b79e3333b45c0136420fcc953d9e5206d500d4d47ce96d6be96 L:05a3a85ac8ccfd1b24329c049483580dcecb30dd24d208b9470c031e1e208341 L:7b5feb4c4ebafd8cae1e786de58f8f98e2cf59417ca6632bc6b17ed99c2d8184
data/c7,md5,b4b5b6ad198fe121905d0779b24414e6,sha256,2e47bf1834c0e6a5a5d4ddc191924a3bbbb28db6add43d206823d81371601934,L:0f4a54d8d5678b878e6c05dc38e64d5f L:73093d69d6202d0ba24ae3ee5fb011d695f550a5e506efcbcef48f61039e983c R:fd0feb0200c97b79e3333b45c0136420fcc953d9e5206d500d4d47ce96d6be96 L:05a3a85ac8ccfd1b24329c049483580dcecb30dd24d208b9470c031e1e208341 L:7b5feb4c4ebafd8cae1e786de58f8f98e2cf59417ca6632bc6b17ed99c2d8184
data/c8,md5,c4035d3557b46523c08dbe4c71a3ad83,sha256,2e47bf1834c0e6a5a5d4ddc191924a3bbbb28db6add43d206823d81371601934,R:25cf473505ff2d411e4108428235524f L:2ed7e0693f37621592014ac576563412a61ae44124e3142717fff4c5ea7e2e7b L:05a3a85ac8ccfd1b24329c049483580dcecb30dd24d208b9470c031e1e208341 L:7b5feb4c4ebafd8cae1e786de58f8f98e2cf59417ca6632bc6b17ed99c2d8184
data/c9,md5,25cf473505ff2d411e4108428235524f,sha256,2e47bf1834c0e6a5a5d4ddc191924a3bbbb28db6add43d206823d81371601934,L:c4035d3557b46523c08dbe4c71a3ad83 L:2ed7e0693f37621592014ac576563412a61ae44124e3142717fff4c5ea7e2e7b L:05a3a85ac8ccfd1b24329c049483580dcecb30dd24d208b9470c031e1e208341 L:7b5feb4c4ebafd8cae1e786de58f8f98e2cf59417ca6632bc6b17ed99c2d8184
```
