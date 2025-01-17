ROOT := ../
SRC := $(ROOT)/dimod/include/

all: catch2 test_main test_main_parallel tests tests_parallel

coverage:
	g++ -std=c++11 -Wall -c test_main.cpp --coverage -fno-inline -fno-inline-small-functions -fno-default-inline
	g++ -std=c++11 -Wall test_main.o tests/*.cpp -o test_main -I $(SRC) --coverage -fno-inline -fno-inline-small-functions -fno-default-inline
	lcov -c -i -b ${ROOT} -d . -o baseline.info
	./test_main
	lcov -c -d . -b ${ROOT} -o test.info
	lcov -a baseline.info -a test.info -o coverage.info
	rm baseline.info test.info
	lcov --remove coverage.info '/usr/*' --output-file coverage.info

tests: test_main.out
	./test_main 

tests_parallel: test_main_parallel.out
	./test_main_parallel

test_main: test_main.cpp
	g++ -std=c++11 -Wall -c test_main.cpp
	g++ -std=c++11 -Wall test_main.o tests/*.cpp -o test_main -I $(SRC)

test_main_parallel: test_main.cpp
	g++ -std=c++11 -fopenmp -Wall -c test_main.cpp -o test_main_parallel.o
	g++ -std=c++11 -fopenmp -Wall test_main_parallel.o tests/*.cpp -o test_main_parallel -I $(SRC)

catch2:
	git submodule init
	git submodule update
