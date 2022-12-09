

## Setting up the AFL Fuzzer
For our project we are fuzzing two separate programs: a [JSON parser](https://github.com/json-parser/json-parser) written by github user James McLaughlin: `https://github.com/json-parser/json-parser` and [Fuzzgoat](https://github.com/fuzzstati0n/fuzzgoat), an intentionally buggy software based on the same JSON parser, writen by `https://github.com/fuzzstati0n/fuzzgoat`. To start fuzzing, there are a few steps:

1. Clone our [repository](https://github.com/dcboules/AFL-182) into any directory:
``https://github.com/dcboules/AFL-182``

2. The fuzzer should already be set up. If not, follow the [tutorial](https://elearn.ucr.edu/courses/67700/files/5116324?module_item_id=1162442) written by our talented TA Spoorthi Badikala: `https://elearn.ucr.edu/courses/67700/files/5116324?module_item_id=1162442`
3. *Possibly optional:* 
We had to deal with this issue but we're not sure if this applies to every user. We had some issues with our memory configuration, and we had to modify the core pattern. This can be done in two ways: 
	You can, as root, modify the core pattern through the command: 
	```"echo core /proc/sys/kernel/core_pattern".```
    Or run the AFL command: 
     ```"export AFL_I_DONT_CARE_ABOUT_MISSING_CRASHES=1".``` 
	Either of these should modify the core pattern and allow fuzzing to start. 
4. To start fuzzing the JSON parser, navigate to `AFL-182/json-parser` and run the following command: 
     `"afl-fuzz -x ../dictionaries/json.dict -i ../inputs/ -o ../outputs/ -m none -- ./test_json -M Fuzz1 @@".`
5. Inputs are taken from sample valid and invalid inputs provided in the JSON parser repository, and results are stored in `AFL-182/outputs`.
6. To start fuzzing Fuzzgoat, navigate to `AFL-182/fuzzgoat` and run the following command: 
	 ```"afl-fuzz -i afl_in -o afl_out ./fuzzgoat @@".```
7. Inputs are taken from random garbage data, and results are stored in `AFL-182/fuzzgoat/afl_out`.
