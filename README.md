MongoDB, Java, PHP, Python, jQuery and JSON Practicals 1–10
Practical 1 - MongoDB Basics:1
A. Write a MongoDB query to create and drop database.
Create Database
use TYITDB239720

Drop Database
db.dropDatabase()

B. Write a MongoDB query to create, display and drop collection.
Create Collection
db.createCollection("Employee")

Display Collection
show collections

Drop Collection
db.Employee.drop()

C. Write a MongoDB query to insert, query, update and delete a document.
Insert Document
db.Employee.insertOne({
    id: 1,
    name: "Romal",
    age: 20,
    city: "Mumbai",
    salary: 25000,
    department: "Developer"
})

Query Document
db.Employee.find()

Update Document
db.Employee.updateOne(
    {id: 1},
    {$set: {salary: 30000}}
)

Delete Document
db.Employee.deleteOne({id: 1})

D. Employee Queries
1) Insert and display the documents in the Employee collection.
db.Employee.insertMany([
    {
        id: 1,
        name: "Romal",
        age: 20,
        city: "Mumbai",
        area: "Kurla",
        salary: 25000,
        department: "Developer"
    },
    {
        id: 2,
        name: "Rahul",
        age: 22,
        city: "Thane",
        area: "Thane",
        salary: 18000,
        department: "Tester"
    },
    {
        id: 3,
        name: "Priya",
        age: 21,
        city: "Mumbai",
        area: "Kurla",
        salary: 19500,
        department: "Tester"
    },
    {
        id: 4,
        name: "Sneha",
        age: 24,
        city: "Mumbai",
        area: "Andheri",
        salary: 12000,
        department: "Developer"
    }
])

db.Employee.find()

2) Display details of employees who live in Mumbai.
db.Employee.find({
    city: "Mumbai"
})

3) Display details of employee staying in Kurla and salary greater than 19000
db.Employee.find({
    area: "Kurla",
    salary: {$gt: 19000}
})

4) Display details of the employee whose salary is greater than equal 10000 but less than 20000.
db.Employee.find({
    salary: {
        $gte: 10000,
        $lt: 20000
    }
})

5) Display details of employees staying in either thane or mumbai and salary greater than 10000.
db.Employee.find({
    city: {$in: ["Thane", "Mumbai"]},
    salary: {$gt: 10000}
})

6) Display details of employee whose salary is not equal to 10000 and working in either developer or tester department.
db.Employee.find({
    salary: {$ne: 10000},
    department: {$in: ["Developer", "Tester"]}
})

Practical 2 - MongoDB Basics:2
3. Insert the documents
db.Users.insertMany([
    {
        FirstName: "Romal",
        Age: 20,
        Gender: "M",
        Country: "India"
    },
    {
        FirstName: "Priya",
        Age: 21,
        Gender: "F",
        Country: "India"
    },
    {
        FirstName: "Sneha",
        Age: 22,
        Gender: "F",
        Country: "USA"
    },
    {
        FirstName: "John",
        Age: 25,
        Gender: "M",
        Country: "USA"
    }
])

4. Update the country to UK for all female users.
db.Users.updateMany(
    {Gender: "F"},
    {$set: {Country: "UK"}}
)

5. Add the new field company to all the documents.
db.Users.updateMany(
    {},
    {$set: {Company: "ABC"}}
)

6. Delete all the documents where Gender = ‘M’.
db.Users.deleteMany({
    Gender: "M"
})

1. Find out a count of female users who stay in either India or USA.
db.Users.countDocuments({
    Gender: "F",
    Country: {$in: ["India", "USA"]}
})

2. Display the first name and age of all female employees.
db.Users.find(
    {Gender: "F"},
    {_id: 0, FirstName: 1, Age: 1}
)
1. Find out a count of female users who stay in either India or USA.
db.Users.countDocuments({
    Gender: "F",
    Country: {$in: ["India", "USA"]}
})

2. Display the first name and age of all female employees.
db.Users.find(
    {Gender: "F"},
    {_id: 0, FirstName: 1, Age: 1}
)
Practical 3 – Aggregate Functions
Insert collection in the database and display all the records.
db.Employee.insertMany([
    {
        name: "Romal",
        department: "Developer",
        salary: 25000,
        age: 20
    },
    {
        name: "Rahul",
        department: "Tester",
        salary: 18000,
        age: 22
    },
    {
        name: "Priya",
        department: "Developer",
        salary: 30000,
        age: 21
    },
    {
        name: "Sneha",
        department: "Tester",
        salary: 22000,
        age: 24
    }
])

db.Employee.find()

1. Group by function to get count.
db.Employee.aggregate([
    {
        $group: {
            _id: "$department",
            count: {$sum: 1}
        }
    }
])

2. Sum function.
db.Employee.aggregate([
    {
        $group: {
            _id: "$department",
            totalSalary: {$sum: "$salary"}
        }
    }
])

3. Avg function.
db.Employee.aggregate([
    {
        $group: {
            _id: "$department",
            averageSalary: {$avg: "$salary"}
        }
    }
])

1. Min function
db.Employee.aggregate([
    {
        $group: {
            _id: "$department",
            minimumSalary: {$min: "$salary"}
        }
    }
])

2. Max function.
db.Employee.aggregate([
    {
        $group: {
            _id: "$department",
            maximumSalary: {$max: "$salary"}
        }
    }
])

3. First function
db.Employee.aggregate([
    {
        $group: {
            _id: "$department",
            firstEmployee: {$first: "$name"}
        }
    }
])

4. Last function
db.Employee.aggregate([
    {
        $group: {
            _id: "$department",
            lastEmployee: {$last: "$name"}
        }
    }
])

5. Push function
db.Employee.aggregate([
    {
        $group: {
            _id: "$department",
            employees: {$push: "$name"}
        }
    }
])

6. addToSet function
db.Employee.aggregate([
    {
        $group: {
            _id: "$department",
            employees: {$addToSet: "$name"}
        }
    }
])
-------------------------------------------
Practical 4 – Java and MongoDB
Your original update program uses the old Java MongoDB API, while the other programs use the newer API. If your college specifically uses the old driver, your original code may be expected.

For a consistent newer-style version:

2. Update the document in MongoDB using Java
import com.mongodb.client.MongoCollection;
import com.mongodb.client.MongoDatabase;
import com.mongodb.MongoClient;
import com.mongodb.client.model.Filters;
import com.mongodb.client.model.Updates;
import org.bson.Document;

public class update {
    public static void main(String[] args) {
        MongoClient mongo = new MongoClient("localhost",27017);
        System.out.println("Connected to the database successfully.");

        MongoDatabase database = mongo.getDatabase("TYITDB239720");
        MongoCollection<Document> collection = database.getCollection("myCol");

        collection.updateOne(
            Filters.eq("id",1),
            Updates.set("Age",27)
        );

        System.out.println("Document updated successfully");
        mongo.close();
    }
}

Output:
Connected to the database successfully.
Document updated successfully
-------------------------------------------------------------
Practical 4 – Java and MongoDB
1. Insert the document in MongoDB using Java.
import com.mongodb.client.MongoCollection;
import com.mongodb.client.MongoDatabase;
import com.mongodb.MongoClient;
import org.bson.Document;

public class insert {
    public static void main(String[] args) {
        MongoClient mongo = new MongoClient("localhost",27017);
        System.out.println("Connected to the database successfully.");
        MongoDatabase database = mongo.getDatabase("TYITDB239720");
        MongoCollection<Document> collection = database.getCollection("myCol");
        System.out.println("Collection myCol selected successfully");
        Document document = new Document();
        document.append("id",1);
        document.append("Name","Romal");
        document.append("RollNo",239720);
        document.append("Age",20);
        document.append("College","MCC");
        collection.insertOne(document);
        System.out.println("Document inserted successfully");
    }
}

Output:
Connected to the database successfully.
Collection myCol selected successfully
Document inserted successfully

2. Update the document in MongoDB using Java.
import com.mongodb.DB;
import com.mongodb.DBCollection;
import com.mongodb.BasicDBObject;
import com.mongodb.MongoClient;
import com.mongodb.WriteResult;
import java.net.UnknownHostException;

public class update {
    public static void main(String[] args) {
        MongoClient mongo = new MongoClient("localhost",27017);
        System.out.println("Connected to the database successfully.");
        DB db = mongo.getDB("TYITDB239720");
        DBCollection col = db.getCollection("myCol");
        BasicDBObject query = new BasicDBObject("id",1);
        BasicDBObject update = new BasicDBObject();
        update.put("$set",new BasicDBObject("Age",27));
        WriteResult result = col.update(query,update);
        mongo.close();
    }
}

Output:
Connected to the database successfully.

3. Retrieve the document in MongoDB using Java
import com.mongodb.client.MongoCollection;
import com.mongodb.client.MongoDatabase;
import com.mongodb.MongoClient;
import com.mongodb.MongoCredential;
import org.bson.Document;
import java.util.Iterator;
import com.mongodb.client.FindIterable;

public class retrieve {
    public static void main(String[] args) {
        MongoClient mongo = new MongoClient("localhost",27017);
        System.out.println("Connected to the database successfully.");
        MongoDatabase database = mongo.getDatabase("TYITDB239720");
        MongoCollection<Document> collection = database.getCollection("myCol");
        System.out.println("Collection myCol selected successfully");
        FindIterable<Document> iterDoc = collection.find();
        int i = 1;
        Iterator it = iterDoc.iterator();
        while(it.hasNext()) {
            System.out.println(it.next());
            i++;
        }
    }
}

Output:
Connected to the database successfully.
Collection myCol selected successfully

4. Delete the document in MongoDB using Java.
import com.mongodb.client.MongoCollection;
import com.mongodb.client.MongoDatabase;
import com.mongodb.MongoClient;
import com.mongodb.MongoCredential;
import org.bson.Document;
import com.mongodb.client.model.Filters;

public class delete {
    public static void main(String[] args) {
        MongoClient mongo = new MongoClient("localhost",27017);
        System.out.println("Connected to the database successfully.");
        MongoDatabase database = mongo.getDatabase("TYITDB239720");
        MongoCollection<Document> collection = database.getCollection("myCol");
        System.out.println("Collection myCol selected successfully");
        collection.deleteOne(Filters.eq("id",1));
        System.out.println("Document deleted successfully");
    }
}

Output:
Connected to the database successfully.
Collection myCol selected successfully
Document deleted successfully

Practical 5 – PHP
php_mongo.dll ---> copy this file and paste it in xampp--> php--> ext

Edit the configuration --> xampp --> php ---> php(Type: Configuration setting)

Save Files at the location: C:\xampp\htdocs

Execute: Open xampp Apache → Start (Make it active) and Admin(Make it active)

Browser will open

Remove dashboard and instead give the name of the file (eg: insert.php)

Output is printed.

1. insert.php
<?php $m = new MongoClient(); echo "Connection to database successfully"; $db = $m -> MYDB239720; echo "\nDatabase selected successfully"; $col = $db -> MyCol; echo "\nCollection selected successfully"; $doc = array( "name" => "Romal", "age" => 20, "dept" => "TYIT", "rollno" => 239720 ); $col -> insert($doc); echo "\nDocument inserted successfully"; ?>

Output:
Connection to database successfully
Database selected successfully
Collection selected successfully
Document inserted successfully

2. update.php
<?php $m = new MongoClient(); echo "Connection to database successfully"; $db = $m -> MYDB239720; echo "\nDatabase selected successfully"; $col = $db -> MyCol; echo "\nCollection selected successfully"; $col -> update(array( "name" => "Romal"),array('$set'=>array("age" => 19))); echo "\nDocument updated successfully"; ?>

Output:
Connection to database successfully
Database selected successfully
Collection selected successfully
Document updated successfully

3. retrieve.php
<?php $m = new MongoClient(); echo "Connection to database successfully"; $db = $m -> MYDB239720; echo "\nDatabase selected successfully"; $col = $db -> MyCol; echo "\nCollection selected successfully"; $cursor = $col -> find(); foreach($cursor as $doc) { echo"<br/>"; echo $doc["name"]."<br/>"; echo $doc["age"]."<br/>"; echo $doc["dept"]."<br/>"; echo $doc["rollno"]."<br/>"; }?>

Output:
Connection to database successfully
Database selected successfully
Collection selected successfully

Romal
20
TYIT
239720

4. delete.php
<?php $m = new MongoClient(); echo "Connection to database successfully"; $db = $m -> MYDB239720; echo "\nDatabase selected successfully"; $col = $db -> MyCol; echo "\nCollection selected successfully"; $col -> remove(array( "name" => "Romal")); echo "\nDocument deleted successfully"; ?>

Output:
Connection to database successfully
Database selected successfully
Collection selected successfully
Document deleted successfully
-----------------------------------------------------------------
Practical 6 – Python
1. Insert
from pymongo import MongoClient

client = MongoClient('localhost',27017)
db = client.TYITDB239720

def insert():
    try:
        name1 = input("Enter the Name:")
        age1 = input("Enter the Age:")
        dept1 = input("Enter the Department:")
        pin1 = input("Enter the Pin No:")

        db.MyCol.insert_one({
            "name":name1,
            "age":age1,
            "dept":dept1,
            "pin":pin1
        })

        print("Inserted data successfully")

    except Exception as e:
        print(str(e))

insert()

2. Update
from pymongo import MongoClient

client = MongoClient('localhost',27017)
db = client.TYITDB239720

def update():
    try:
        name1 = input("Enter the Name:")
        age1 = input("Enter the Age to update:")

        db.MyCol.update_one(
            {"name":name1},
            {"$set":{"age":age1}}
        )

        print("\nRecords updated successfully\n")

    except Exception as e:
        print(str(e))

update()

3. Retrieve
from pymongo import MongoClient

client = MongoClient('localhost',27017)
db = client.TYITDB239720

def read():
    try:
        Col = db.MyCol.find()

        print("\nAll data from database TYITDB239720:")

        for MyCol in Col:
            print(MyCol)

    except Exception as e:
        print(str(e))

read()

4. Delete
from pymongo import MongoClient

client = MongoClient('localhost',27017)
db = client.TYITDB239720

def delete():
    try:
        name1 = input("Enter the name:")

        db.MyCol.delete_one({"name":name1})

        print("\nData deleted successfully")

    except Exception as e:
        print(str(e))

delete()
------------------------------------------------------------
Practical 6 – Python
1. insert
from pymongo import MongoClient
client = MongoClient('localhost',27017)
db = client.TYITDB239720
def insert(): try: name1 = input("Enter the Name:") age1 = input("Enter the Age:") dept1 = input("Enter the Department:") pin1 = input("Enter the Pin No:") db.MyCol.insert_one({ "name":name1, "age":age1, "dept":dept1, "pin":pin1 }) print("Inserted data successfully") except Exception: print(str(e)) insert()

Output:
Enter the Name:
Enter the Age:
Enter the Department:
Enter the Pin No:
Inserted data successfully

2. update()
from pymongo import MongoClient
client = MongoClient('localhost',27017)
db = client.TYITDB239720
def update(): try: name1 = input("Enter the Name:") age1 = input("Enter the Age to update:") db.MyCol.update_one({"name":name1},{"$set":{"age":age1}}) print("\nRecords updated successfully\n") except Exception: print(str(e)) update()

Output:
Enter the Name:
Enter the Age to update:

Records updated successfully

3. Retrieve
from pymongo import MongoClient
client = MongoClient('localhost',27017)
db = client.TYITDB239720
def read(): try: Col = db.MyCol.find() print("\nAll data from database TYITDB239720:") for MyCol in Col: print(MyCol) except Exception: print(str(e)) read()

Output:
All data from database TYITDB239720:

4. delete
from pymongo import MongoClient
client = MongoClient('localhost',27017)
db = client.TYITDB239720def delete(): try: name1 = input("Enter the name:") db.MyCol.delete_one({"name":name1}) print("\nData deleted successfully") except Exception: print(str(e)) delete()

Output:
Enter the name:

Data deleted successfully
---------------------------------------------------------------------
Practical 7 – jQuery
3. Click, hover, on, trigger, off
The corrected version of the problematic part is:

<!DOCTYPE html>
<head>
    <title>Basic jQuery</title>
    <script src="jquery-3.6.1.min.js"></script>
    <script>
        $(document).ready(function () {

            $("#b1").hover(function(){
                document.write("Hello Romal")
            })

            $("p").on("click", function() {
                $(this).css("background", "yellow");
            });

            $("#b2").click(function(){
                $("p").off("click");
            });

            $("#b3").on("click", function(){
                $("#t1").hide();
            });

            $("input").select(function(){
                $("input").after("Text Marked!")
            });

            $("#b4").click(function(){
                $("input").trigger("select");
            });

        })
    </script>
</head>
<body>

    <button id="b1">Hover</button><br>
    <p>Welcome to the Mulund College</p><br>

    <p>Romal: 239720</p><br>

    <button id="b2">Off</button><br>

    <p id="t1">Hello Romal</p><br>

    <button id="b3">On</button><br>

    <input type="text" value="Romal 239720"><br>

    <button id="b4">Trigger</button><br>

</body>

Slide Toggle
Remove the extra s:

<button>Slide Toggle</button>
-------------------------------------------------------------

Practical 7 – jQuery
1. Write a jQuery to check the contents of the elements on the button click.
<!DOCTYPE html>
<head>
    <title>Basic jQuery</title>
    <script src="jquery-3.6.1.min.js"></script>
    <script>
        $(document).ready(function () {
            $("#btn").click(function(){
                document.write("Hello Romal")
            })
        })
    </script>
</head>
<body>
    <p>Romal: 239720</p>
    <button id="btn">Click Me</button>
</body>

Output:
Hello Romal

2. Write a jQuery to select elements by class name, id and element names.
<!DOCTYPE html>
<head>
    <title>Basic jQuery</title>
    <script src="jquery-3.6.1.min.js"></script>
    <script>
        $(document).ready(function() {
            $(".class1").css("background","lightblue");
            $("#id1").css("background","pink");
            $("h2").css("background", "lightgreen");
        })
    </script>
</head>
<body>
    <p class="class1">Romal: 239720</p>
    <p id="id1">Romal Shah</p>
    <h2>Welcome Romal</h2>
</body>

Output:
Romal: 239720
Romal Shah
Welcome Romal

The backgrounds are changed to:

Romal: 239720 → lightblue
Romal Shah → pink
Welcome Romal → lightgreen

3. Write jQuery to show the use of click(), hover(), on(), trigger(),off() events.
<!DOCTYPE html>
<head>
    <title>Basic jQuery</title>
    <script src="jquery-3.6.1.min.js"></script>
    <script>
        $(document).ready(function () {
            $("#b1").hover (function(){
            document.write("Hello Romal")
            })
            $("p").on("click", function() {
                $(this).css("background", "yellow");
            });
            $("#b2").click(function(){
                $("p").off("click");
            });
            $("#b3").on(function(){
                $("#t1").hide();
            });
            $("input").select(function(){
                $("input").after("Text Marked!")
            });
            $("#b4").click(function(){
                $("input").trigger("select");
            });
        })
    </script>
</head>
<body>
    <button id="b1">Hover</button><br><p>Welcome to the Mulund College</p><br>
    <p>Romal: 239720</p><br>
    <button id="b2">Off</button><br>
    <p id="t1">Hello Romal</p><br>
    <button id="b3">On</button><br>
    <input type="text" value="Romal 239720"><br>
    <button id="b4">Trigger</button><br>
</body>

Output:
Hover: Click, on, offTrigger:

4. Write a jQuery to create animated show hide effect.
<!DOCTYPE html>
<head>
<title>Basic jQuery</title>
<script src="jquery-3.6.1.min.js"></script>
<script>
$(document).ready(function(){
    $("#b1").click(function(){
        $("p").hide();
    });
    $("#b2").click(function(){
        $("p").show();
    })
})
</script>
</head><body>
<p>Romal Shah:239720</p>
<button id="b1">Hide</button>
<button id="b2">Show</button>
</body>

Output:
Click Hide → Paragraph disappears
Click Show → Paragraph appears

5. Write a jQuery to create a simple toggle effect.
<!DOCTYPE html>
<head>
<title>Basic jQuery</title>
<script src="jquery-3.6.1.min.js"></script>
<script>
$(document).ready(function(){
    $("button").click(function(){
        $("p").toggle();
    });
})
</script>
</head>
<body>
<p>Romal Shah:239720</p><button>Toggle</button>
</body>

Output:
Click Toggle → Paragraph disappears
Click Toggle again → Paragraph appears

6. Write a jQuery to create fade-in and fade-out effect.
<!DOCTYPE html>
<head>
<title>Basic jQuery</title>
<script src="jquery-3.6.1.min.js"></script>
<script>
$(document).ready(function(){
    $(".c1").click(function(){
        $("p").fadeOut(5000);
    });
    $(".c2").click(function(){
        $("p").fadeIn(5000);
    })
})
</script>
</head>
<body>
<p>Romal Shah:239720</p>
<button class="c1">Fade Out</button><button class="c2">Fade In</button>
</body>

Output:
Click Fade Out → Paragraph fades out
Click Fade In → Paragraph fades in

7. Write a jQuery to create fade toggle effect.
<!DOCTYPE html>
<head>
<title>Basic jQuery</title>
<script src="jquery-3.6.1.min.js"></script>
<script>
$(document).ready(function(){
    $("button").click(function(){
        $("p").fadeToggle(5000);
    });
})
</script>
</head>
<body>
<p>Romal Shah:239720</p>
<button>Fade Toggles</button>
</body>

Output:
Click Fade Toggles → Paragraph fades out
Click again → Paragraph fades in

8. Write a jQuery to create slide-up and slide-down effect.
<!DOCTYPE html>
<head>
<title>Basic jQuery</title>
<script src="jquery-3.6.1.min.js"></script>
<script>
$(document).ready(function(){
    $("#b1").click(function(){
        $("p").slideUp(3000);
    });
    $("#b2").click(function(){
        $("p").slideDown(3000);
    })
})
</script>
</head>
<body>
<p>Romal Shah:239720</p>
<button id="b1">Slide Up</button>
<button id="b2">Slide Down</button>
</body>

Output:
Click Slide Up → Paragraph slides up
Click Slide Down → Paragraph slides down

9. Write a jQuery to create slide toggle effect.
<!DOCTYPE html>
<head>
<title>Basic jQuery</title>
<script src="jquery-3.6.1.min.js"></script>
<script>
$(document).ready(function(){
    $("button").click(function(){
        $("p").slideToggle(5000);
    })
})
</script>
</head>
<body>
<p>Romal Shah:239720</p>
<button>Slide Toggle</button>s
</body>

Output:
Click Slide Toggle → Paragraph slides up/down

10. Write a jQuery to create Mouse Event.
<!DOCTYPE html>
<html>
<head>
<title>Basic jQuery</title>
<script src="jquery-3.6.1.min.js"></script>
<script>
$(document).ready(function(){
    $("#p1").mouseleave(function(){
        alert("Bye! You now leave p1");
    })
})
</script>
</head>
<body>
<p id="p1">This is a paragraph</p>
</body>
</html>

Output:
Bye! You now leave p1
----------------------------------------------------------------
Practical 8 – jQuery Animation
2. Animate multiple CSS properties
Your original code had:

l eft:"150"

and:

position:rela tive;

Correct code:

<html>
<head>

<script src="jquery-3.6.1.min.js"></script>

<script>
$(document).ready(function(){
    $("#b1").click(function(){
        $("#div1").animate({
            width:"150px",
            height:"150px",
            opacity:"0.5",
            left:"150px"
        });
    })
})
</script>

<style>
#div1{
    width:100px;
    height:100px;
    background:yellow;
    position:relative;
}
</style>

</head>

<body>

<p> Animation</p>

<div id="div1"></div>

<button id="b1">Click to Animate</button>

</body>
</html>-----------------------------------------
--------------------------------------------------------
Practical 8
1. Write a jQuery to create animation effect.
<!DOCTYPE html>
<head>
<title>Basic jQuery</title>
<script src="jquery-3.3.1.min.js"></script>
<script>
$(document).ready(function(){
    $("button").click(function(){
        $("img").animate({left:50});
    })
})
</script>
<style>
img{position:relative;}
</style>
</head>
<body>
<p>Romal:239720</p>
<img src="Mountain.png" alt="Mountain Image"><br>
<br><button>Start Animation</button>
</body>

Output:
Mountain image moves to the left position 50 when Start Animation is clicked.

2. Write a jQuery to animate multiple css properties.
<html>
<head>
<script src="jquery-3.6.1.min.js"></script><script>
$(document).ready(function(){
    $("#b1").click(function(){
        $("#div1").animate({width:"150px",height:"150px",opacity:"0.5",l eft:"150"});
    })
})
</script>
<style>
#div1{width:100px;height:100px;background:yellow;position:rela tive;}
</style>
</head>
<body>
<p> Animation</p>
<div id="div1"></div>
<button id="b1">Click to Animate</button>
</body>
</html>

Output:
A yellow square is displayed.
After clicking Click to Animate, the square is animated.

3. Write a jQuery to perform method of chaining.
<!DOCTYPE html>
<head>
<title>Basic jQuery</title>
<script src="jquery-3.3.1.min.js"></script>
<script>
$(document).ready(function(){
    $("button").click(function(){
        $("#p1").css("color","blue").slideUp(2000).slideDown(2000)
    })
})
</script>
</head>
<body>
<p id="p1">Romal:239720</p>
<button>Click Me</button>
</body>

Output:
Romal:239720

The text changes to blue.
The paragraph slides up and then slides down.

Practical 9
1. Write a jQuery effect method with a callback function.
<!DOCTYPE html>
<head>
<title>Basic jQuery</title>
<script src="jquery-3.3.1.min.js"></script>
<script>
$(document).ready(function(){
    $("button").click(function(){
        $("p").hide("slow",function(){
            alert("The paragraph is now hidden")
        })
    })
})
</script>
</head>
<body>
<p>Romal:239720</p>
<p>Welcome to MCC</p>
<button>Click!</button>
</body>

Output:
The paragraph is now hidden

2. Write a jQuery to get and set text context of the elements.
<!DOCTYPE html>
<head>
    <title>Basic jQuery</title>
    <script src="jquery-3.6.1.min.js"></script>
    <script>
        $(document).ready(function(){
            $("#b1").click(function(){
                var str = $("p").text();
                alert(str);
            })
            $("#b2").click(function(){
                $("p").text("Hello World");
            })
        })
    </script>
</head><body>
<p>Romal Shah:239720</p>
<p> MongoDB</p>
<button id="b1">Get</button>
<button id="b2">Set</button>
</body>

Output:
Click Get:

Romal Shah:239720
 MongoDB

Click Set:

Hello World

3. Write a jQuery to get and set HTML contents of the elements.
<!DOCTYPE html>
<head>
<title>Basic jQuery</title><script src="jquery-3.6.1.min.js"></script>
<script>
$(document).ready(function(){
$("#b1").click(function(){
var str = $("p").html();
alert(str);
})
$("#b2").click(function(){
$("p").html("<b>Hello World<b>");
})
})
</script>
</head>
<body>
<p><b>Romal Shah:</b><u>239720</u></p>
<p> MongoDB</p>
<button id="b1">Get</button>
<button id="b2">Set</button>
</body>

Output:
Click Get:

Romal Shah:239720

Click Set:

Hello World

Practical 10 – JSON
1. Creating JSON
<html>
<head>
<title>Creating JSON</title>
</head>
<body>
<script type="text/javascript">
var data={
"name":"Romal",
"age":20,
"dept":"IT"
}
document.writeln(JSON.stringify(data)+"</br>");
document.writeln(JSON.stringify(data,["name","age","dept"]) +"<br/>");
document.writeln(JSON.stringify(data,["name","age","dept"], 5));
</script>
</body>
</html>

Output:
{"name":"Romal","age":20,"dept":"IT"}

{"name":"Romal","age":20,"dept":"IT"}

{
     "name": "Romal",
     "age": 20,
     "dept": "IT"
}

2. Parsing JSON
<html>
<body>
<script type="text/javascript">
var data = '{"name":"Romal","age":20,"dept":"IT"}';
var jsonObj = JSON.parse(data, function(name, value) {
return value;
});document.writeln(jsonObj.name); for (key in jsonObj) { document.writeln("<br/>" + key + " : " + jsonObj[key]); } var jsonObj = JSON.parse(data, function(name, value) { if (name == "sem") { return undefined; } else { return value; } }); for (key in jsonObj) { document.writeln("<br/>" + key + " : " + jsonObj[key]); } </script> </body> </html>

Output:
Romal

name : Romal
age : 20
dept : IT

name : Romal
age : 20
dept : IT

3. Parsing JSON
<html>
<body>
<script type="text/javascript">
var data = '{"name":"Romal","age":20,"dept":"IT"}';var obj = JSON.parse(data); for(var key in obj) { document.writeln(“<br/>+”key+":"+obj[key]); } </script> </body> </html>

Output:
name:Romal
age:20
dept:IT
------------------------------------------------------------
Practical 10 – JSON
3. Parsing JSON
Your original line:

document.writeln(“<br/>+”key+":"+obj[key]);

is incorrect.

Use:

<html>
<body>

<script type="text/javascript">

var data = '{"name":"Romal","age":20,"dept":"IT"}';

var obj = JSON.parse(data);

for(var key in obj) {
    document.writeln("<br/>" + key + ":" + obj[key]);
}

</script>

</body>
</html>

Output:
name:Romal
age:20
dept:IT
------------------------------------------------------------------------
