CFLAGS= -fprofile-arcs -ftest-coverage -fPIC

all:
	mkdir -p build
	$(CXX) $(CFLAGS) -c src/file1.cpp -o build/file1.o
	$(CXX) $(CFLAGS) -c src/main.cpp -o build/main.o
	$(CXX) $(CFLAGS) build/main.o build/file1.o -o build/testcase

run: txt xml html sonarqube json_summary coveralls


coverage.json:
	build/testcase
	$(GCOVR) --json $@

txt: coverage.json
	$(GCOVR) -a $< -o coverage.txt

xml: coverage.json
	$(GCOVR) -a $< -x -o coverage.xml

html: coverage.json
	$(GCOVR) -a $< --html-details -o coverage.html

sonarqube: coverage.json
	$(GCOVR) -a $< --sonarqube sonarqube.xml

coveralls: coverage.json
	$(GCOVR) -a $< --coveralls coveralls.json

json_summary:
	build/testcase
	$(GCOVR) $(GCOVR_TEST_OPTIONS) -d --json-summary -o summary_coverage.json

clean:
	rm -f build/*
	rm -f coverage*.* sonarqube*.* summary_coverage.json coveralls.json
