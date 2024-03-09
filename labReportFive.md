## Lab Report Five - Putting It All Together

# Part 1 - Debugging Scenario
1. **Original Student Post**
  ![122553.png]
  Hello, I am recieving this error whenever I attempt to run my bash grading script. The `TestListExamples` file that I am testing does have a main method so I believe that the error occurs when the file is being run and java can't find the main method.

2. **TA Rsponse**
  I think that you are correct with and there does lie within what you are passing to the `java` command. Try using the `echo` method with the input of the `java` method to see what is being passed into the command.

3. **Bug**
   ![125537.png]
   When running the `echo` command with `-cp $CPATH$JUNIT TestListExamples`, I get the above output. The bug is that there is no space between the `CPATH` and `JUNIT` variables which causes an error in Java finding the main method.

4. **Information**
   \
   File and Directory Strucutre:
```
    │   grade.sh
    │   GradeServer.java
    │   Server.java
    │   TestListExamples.java
    │
    ├───grading-area
    │   │   IsMoon.class
    │   │   junit-output.txt
    │   │   ListExamples.class
    │   │   ListExamples.java
    │   │   StringChecker.class
    │   │   TestListExamples.class
    │   │   TestListExamples.java
    │   │
    │   └───lib
    │           hamcrest-core-1.3.jar
    │           junit-4.13.2.jar
    │
    ├───lib
    │       hamcrest-core-1.3.jar
    │       junit-4.13.2.jar
    │
    └───student-submission
            ListExamples.java
```
Contents of File Before Fixing Bug:

```
CPATH='.;lib/hamcrest-core-1.3.jar;lib/junit-4.13.2.jar'
JUNIT='org.junit.runner.JUnitCore'

rm -rf student-submission
rm -rf grading-area

mkdir grading-area

git clone $1 student-submission
echo 'Finished cloning'

if [ -f "student-submission/ListExamples.java" ]; then 
    echo "file found!"
else 
    echo "ListExamples.java not found!"
    exit 1
fi

cp -r lib grading-area
cp student-submission/ListExamples.java grading-area/
cp TestListExamples.java grading-area/

cd grading-area
javac -cp $CPATH *.java

if [ $? -ne 0 ]; then
    echo "Complie error!"
    exit 1
else
    echo "Compiled successfully!"
fi

java -cp $CPATH$JUNIT TestListExamples > junit-output.txt
lastline=$(cat junit-output.txt | tail -2)
ok=$(grep -o "OK" junit-output.txt)

if [[ "$ok" =~ "OK" ]]; then
    tests=$(echo $lastline | awk -F'[ (]' '{print $3}')
    echo "Your score is $tests / $tests "
else 
    tests=$(echo $lastline | awk -F'[, ]' '{print $3}')
    failures=$(echo $lastline | awk -F'[, ]' '{print $6}')
    successes=$(( tests - failures ))
    echo "Your score is $successes / $tests"
fi
```
Command Line Ran to Trigger Bug:
`$ bash grade.sh https://github.com/ucsd-cse15l-f22/list-methods-corrected`
\
Fixing the Bug:
\
To fix the bug, I had to add a space between the `CPATH` and `JUNIT` variables in the `java` command to run the files. 

