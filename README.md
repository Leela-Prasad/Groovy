for(int i=1;i<5;++i) {
    println i
}

for(i in 1..5) {
    println i
}

for(i in [1,2,3,4,5]) {
    println i
}

1.upto(5) {
    println "$it"
}


1.step(10,3) {
    println "$it"
}

5.times {
    println "$it"
}

int sum = 0;
for(i in [1,2,3,4,5]) {
    sum += i
}
println(sum)

def map = ["abc":1, "def":2, "ghi":3]
for(i in map) {
    println i.value
}


In Groovy Interpolation works with “” strings
Interpolation will not work ‘’ strings
“””””” are used to define strings in multiple lines.
‘’’’’’ are used to define multi line strings but interpolation will not work.
/…/ - used when we want to eliminate escape characters
Here escape character is \
eg: def str = “Hello \“Leela\””
    def str2 = /Hello “Leela”/
$/…/$
Here escape character is $


Methods:
def printHello() {
    println "Hello!!!"
}

printHello()

def add(int a, int b=20) {
    println "sum is " + (a+b)
}

add(5)


def sub(int a, int b) {
    return (a-b)
}

println "Sub is " + sub(20,5)


Closures:
In Java Lambda can either start with { or ()
but in groovy closure should start with {

while calling a method which accept closure parenthesis are optional
list.each({ele -> println ele})
or
list.each {ele -> println ele}

//Supplier
def closure = {println "Hello"}
closure.call()

//Function
def closure2 = {name -> println "Hello ${name}"}
closure2.call("Leela")

//Closure can take outside values also
def str="Hello"
def closure3 = {name -> println "${str} ${name}"}
closure3.call("Leela")


def passingClosuresToMethod(closure) {
    closure.call("Groovy")
}
passingClosuresToMethod(closure2)

def closure4 = {
    a,b,c -> return (a+b+c)
}
println closure4(10,20,30)


def list = ["a", "b", "c"]
//list.each({ele -> println ele})
list.each {ele -> println ele}

def map = ["subject":"groovy", "topic":"closures"]
map.each {entry -> println entry.key + " :: " + entry.value}

def list2 = [1,2,3,4,5]
println list2.find {ele -> ele==3}
println list2.findAll {ele -> ele>=3}
println list2.any {ele -> ele>3}
println list2.every {ele -> ele>0}
println list2.collect {ele -> ele*2}


Collections:
List:
//We can access list via index or using get method.
def fruits = ["Apples", "Oranges", "Grapes"]
println fruits[1]
println fruits.get(2)

def myList = [1,2,3,['A','B',"Groovy"],4]
println myList[1]
println myList[3]

println myList[3][1]
println myList.get(3).get(2)

println myList[0..2]
println myList[4..3]

println myList.contains("Groovy")
println myList[3].contains("Groovy")

println myList[3].size()

// Adding Elements to list
myList.add(10);
println myList

myList<<20
println myList

myList.add(2,22)
println myList

myList.remove(2)
println myList

myList = myList + [30,40]
println myList

myList = myList.plus([50,60])
println myList

myList = myList - [30,40]
println myList

myList = myList.minus([50,60])
println myList

myList.pop()
println myList

println myList.intersect([2,3,6])

println myList.reverse()

println myList.sort()

myList.clear()
println myList.isEmpty()

Map:
def employee = ['name': 'John', 'age': 40]

println employee
println employee.get("name")
println employee.name
println employee["name"]

println employee.size()

employee.put("city", "BZA")
println employee

println employee.getClass()

println employee.containsKey("city")
println employee.containsValue("BZA")

def emp2 = employee.clone()
println emp2

employee.each {entry -> println entry.key + " : " + entry.value}
employee.each {entry -> println "$entry.key : $entry.value"}
employee.eachWithIndex{entry, i -> println("$i | $entry.key : $entry.value")}

employee.each {key,value -> println "$key : $value"}
employee.eachWithIndex{ key,value,i -> println "$i | $key : $value"} 

def entries = employee.entrySet()
entries.each {entry -> assert entry.key in ['name', 'age', 'city']
                       assert entry.value in ['John', 'BZA', 40]
                      }

employee.clear()
println employee

Range:
def range = 1..10
def range2 = 'a..z'
def range3 = 10..1

println range.size()

println range.getFrom()
println range.getTo()

println range.get(3)
println range[3]

println range.contains(6)

println range.isReverse()

def range4 = range.subList(3,8)
println range4.getFrom()
println range4.getTo()

for(i in range) {
    println i
}

println "========="
range.each {
    i -> println i
}


Input Output:
print "Enter your name : "
def name = System.console().readLine()
println "Hello $name"

print "Enter First Number : "
def num1 = System.console().readLine().toInteger()
print "Enter Second Number : "
def num2 = System.console().readLine().toInteger()
println "$num1 + $num2 = " + (num1+num2)

def name="prasad"
println "My Name is $name"

printf "My Name is %s \n", name

printf "%s | %s | %d | %.2f \n", ["Prasad", "Leela", 20, 20.2356]
printf "%-10s | %10s | %d | %.2f \n", ["Prasad", "Leela", 20, 20.2356]

Reading File:
File file = new File("data.txt")
println file.getText()
//or
//println file.text

//Storing all lines from a file
def fileList = file.readLines()
println fileList

def fileList2 = file.collect {it}
println fileList2

def fileArray = file as String[]
println fileArray

//Iterating Each Line in a file
file.eachLine {
    line -> println line
}

// Iterating Each Line in a file with Line Number
file.eachLine {
    line,lineNo -> println "$lineNo | $line"
}

//Iterating Each line with Reader
def line
file.withReader {
    reader -> while((line=reader.readLine())!=null) {
        println line
    }
}

//file content as Bytes
byte[] content = file.getBytes()
println content


println file.isFile()
println file.isDirectory()

//Iterating Files in a Directory
new File("/Users/Leela/Desktop/docker github upload").eachFile {
    eachFile -> println eachFile.getAbsolutePath()
}

println "========"

//Iterating Files in a Directory Recursively
new File("/Users/Leela/Desktop/docker github upload").eachFileRecurse {
    eachFile -> println eachFile.getAbsolutePath()
}

//Copying File contents to another file
def newFile = new File("output.txt")
newFile << file.text

//Deleting a File
newFile.delete()


Writing Files
File myFile = new File("data1.txt")

myFile.write("Line1")
myFile << "\nLine2"

//replaces existing file content
//myFile.text = "File Content"

//replaces existing file content
myFile.withWriter {
    writer -> writer.write("New File Content")
}

myFile.append("\nAnother Line")

println myFile.isFile()
println myFile.isDirectory()
println myFile.isHidden()
println myFile.length()

println myFile.text

def newFile = new File("data2.txt")
newFile << myFile.text

myFile.delete()

newFile.renameTo("output.txt")

Pattern Matching:
def str = "Groovy"

def match = (str =~ "i")
println match
if(match) {
    def i = 0
    while(match) {
        //println match
        println match[i]
        ++i
    }
}else {
    println "No Match"
}
