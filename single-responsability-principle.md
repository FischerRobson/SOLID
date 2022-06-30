## Sigle Responsability Principle (SRP)
Every software component should have one and only responsability (or reason to change). <br/>
Heigher cohesion helps attain better adherence to SRP. <br/>
Loose coupling helps attain better adherence to the SRP. <br/>

An example of SRP:

```java
public class Square {

    int size = 5;

    public int calculateArea() {
        return size * size;
    }

    public int calculatePerimeter() {
        return size * 4;
    }

    public void draw() {
        if (highResolutionMonitor) {
            // render high resolution image of a square
        } else {
            // render normal image of a square
        }
    }

    public void rotate(int degree) {
        // rotate the square clockwise and re-render
    }
}
```

So there a high level of cohesion between calculateArea and calculatePerimeter, and between draw and rotate, but these 2 grups hasn't cohesion, since the first deals with measurements and the second with render images:

```java
public class Square {

    int size = 5;

    public int calculateArea() {
        return size * size;
    }

    public int calculatePerimeter() {
        return size * 4;
    }
}

public class SquareUI {
  
    public void draw() {
        if (highResolutionMonitor) {
            // render high resolution image of a square
        } else {
            // render normal image of a square
        }
    }

    public void rotate(int degree) {
        // rotate the square clockwise and re-render
    }
}
```

Other example is, a student class don't need to know the low level implementation of save method:

```java
public class Student {

    private String studentId;
    private Date studendDOB;
    private String address;

    public String getStudentId() {
        return this.studentId;
    }

    public void setStudentId(String newId) {
        this.studentId = newId;
    }

    public void save() {
        // serialize the object
        try {
            // connect do DB
            // execute insert
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

So, removing the implementation of save from Student to a repository class:

```java
public class Student {

    private String studentId;
    private Date studendDOB;
    private String address;

    public String getStudentId() {
        return this.studentId;
    }

    public void setStudentId(String newId) {
        this.studentId = newId;
    }

    public void save() {
        new RepositoryStudent().save(this);
    }
}

public class RepositoryStudent {
    public void save(Student student) {
        // serialize the object
        try {
            // connect do DB
            // execute insert
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

Other important concept on the last example is the *reasons to change*, supposing you need to change:
* Student ID formtat;
* Student Name format;
* A change in database backend;

So, considering the first two changes like a student data change, there 2 reasons to change, but using this to the example with student and repository class,
there will be just one reason for change on each one.
