---
layout: post
title: 'Udemy Spring boot course: Section 9 JPA / Hibernate advanced mappings'
date: 2023-10-13 11:09 -0500
categories: [Udemy, Java, Springboot, JPA, Hibernate]
tags: [Java, Programming, Udemy, Spring] 
image: 
  path: /2023-10-13-udemy-spring-boot-course-section-9-jpa-hibernate-advanced-mappings/profile.png
---
- [Git repo for this sections code](#git-repo-for-this-sections-code)
- [Course Diagram](#course-diagram)
- [Entity Lifecycle](#entity-lifecycle)
- [Important Database concepts](#important-database-concepts)
  - [Primary Key , Foreign Key](#primary-key--foreign-key)
  - [Cascade](#cascade)
  - [Eager , Lazy Loading](#eager--lazy-loading)
    - [Default Fetch Types](#default-fetch-types)
    - [More about Lazy Loading](#more-about-lazy-loading)
      - [Lazy Loading method 1](#lazy-loading-method-1)
      - [Lazy Loading method 2 (Join Fetch)](#lazy-loading-method-2-join-fetch)
    - [Lazy loading error "Hibernate could not initialize proxy – no Session"](#lazy-loading-error-hibernate-could-not-initialize-proxy--no-session)
  - [Uni-Directional , Bi-Directional](#uni-directional--bi-directional)
- [Association Mappings](#association-mappings)
  - [One-to-One](#one-to-one)
  - [One-to-Many](#one-to-many)
  - [Many-to-Many](#many-to-many)
- [@JoinColumn explained](#joincolumn-explained)
- [mappedBy](#mappedby)
- [Examples](#examples)
  - [Instructor / instructor detail examle](#instructor--instructor-detail-examle)
  - [Instructor Course example](#instructor-course-example)
  - [Adding custom method when extending JpaRepository](#adding-custom-method-when-extending-jparepository)
- [Many to Many implementation](#many-to-many-implementation)


# Git repo for this sections code
  - [git repo](https://github.com/TrestenPool/SpringTutorial/tree/main/Section9)

# Course Diagram
  - ![alt-text](/2023-10-13-udemy-spring-boot-course-section-9-jpa-hibernate-advanced-mappings/uni-directional.png)
  

# Entity Lifecycle
  - [hibernate entity life cycle](https://www.baeldung.com/hibernate-entity-lifecycle)
  - Every Hibernate entity naturally has a lifecycle within the framework – it’s either in a transient, managed, detached or deleted state.

| Operations        | Description                                                                                                                                                                           |
| :---------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| New / Transient   | An entity instance that has been created but is not yet managed by the persistence context. It is not associated with a database record.                                              |
| Detach            | An entity instance that was once managed but is no longer associated with the persistence context. Changes to a detached entity are not automatically synchronized with the database. |
| Merge             | will reattach to hibernate session                                                                                                                                                    |
| Persist / managed | An entity instance that is actively managed by the persistence context and is associated with a database record. Changes to a managed entity will be synchronized with the database.  |
| Removed           | An entity instance marked for deletion.                                                                                                                                               |
| Refresh           | Reload / sync object with data from db. Prevents stale data                                                                                                                           |

  - ![alt-text](/2023-10-13-udemy-spring-boot-course-section-9-jpa-hibernate-advanced-mappings/entity_lifecycle.png)

# Important Database concepts

## Primary Key , Foreign Key
  - Primary Key
    - Unique identifer for a row in a table
  - Foreign Key
    - Field in one table that refers to the primary key in another table
  
  - Referential Integerity
    - preserves relationship between tables
    - prevents operations that would destroy relationships
    - can only contain valid reference to primary key in another table
  
Example below shows how to create a foreign key in MySQL
```sql
CREATE TABLE orders (
    order_id INT AUTO_INCREMENT PRIMARY KEY,
    quantity INT,
    product_id INT,
    FOREIGN KEY (product_id) REFERENCES products(id)
);
```

## Cascade
  - Cascade
    - You can apply the same operation to related entities
  - ![alt-text](/2023-10-13-udemy-spring-boot-course-section-9-jpa-hibernate-advanced-mappings/cascade.png)
    - if we save the instructor, if were to cascade we would also save the instructor detail
    - by the same token if we were to delete an instructor we would delete the instructor detail if it is one-to-one
  - by default no operations are cascaded

| Cascade Type | Description                                                                              |
| :----------- | :--------------------------------------------------------------------------------------- |
| Persist      | if entity is persisted / related entity will also be persisted                           |
| Remove       | if entity is removed / related entity will also be removed                               |
| Refresh      | if entity is refreshed / related entity will also be refreshed                           |
| Detach       | if entity is detached (not associated w/ session) / related entity will also be detached |
| Merge        | if entity is merged / related entity will also be merged                                 |
| All          | All the above cascade types                                                              |


## Eager , Lazy Loading
  - When fetch data, should we retrieve all of the results or just a subset of the results
  - **Eager**
    - Retrieve **all** of the results
  - **Lazy**
    - Retrieve on **Request**

### Default Fetch Types
| Mappping  | Contact         |
| :-------- | :-------------- |
| @OneToOne | FetchType.EAGER |
| @ManyToOne | FetchType.EAGER |
| @OneToMany | FetchType.LAZY |
| @ManyToMany | FetchType.LAZY |

### More about Lazy Loading
  - lazy loading required an **open Hibernate session**
  - need a connection to a database to retrieve data
  - if the hibernate session is closed and you attempt to retrieve lazy data, hibernate will throw an exception

#### Lazy Loading method 1
  - implmenting lazy loading i quite easy
    - all you do is have to specifiy to lazy loading in the entity class
    - if you want to access the elements of a lazy loaded element you have to do it separately and associate them separately

Entity Course class
```java
@ManyToOne(cascade = {CascadeType.PERSIST, CascadeType.MERGE, CascadeType.DETACH, CascadeType.REFRESH})
@JoinColumn("instructor_id")
private Instructor instructor;
``` 

Entity Instructor class
```java
// this is the variable in the Course class that joins the two tables together
@OneToMany(mappedBy="instructor")
private List<Course> courses;
```

Course Repository
```java
public interface CourseRepository extends JpaRepository<Course, Integer> {
    @Query(value = "SELECT * FROM course where instructor_id = ?1",
    nativeQuery = true)
    List<Course> findCoursesByInstructorId(int instructor_id);
}
```

```java
public void getCourses(InstructorServiceImpl instructorService) {
  // other implmenetatoin

    // get the courses separately
    List<Course> courseList = instructorService.getCourseRepository().findCoursesByInstructorId(instructor_id);
    // associate the courses to the instructor
    instructor.get().setCourses(courseList);

    // print out all of the courses for the instructor
    for(var course : instructor.get().getCourses()) {
      System.out.println(course);
    }
  }
}
```

#### Lazy Loading method 2 (Join Fetch)
  - [stack overflow fetch](https://stackoverflow.com/questions/15359306/how-to-fetch-fetchtype-lazy-associations-with-jpa-and-hibernate-in-a-spring-cont)
  - the previous method really sucks, lets be honest, you have to fetch the data separately then associate the data with the object
  - wouldn't it be cool if we could write a single query and it does it all for us
    - WELL WE CAN, AND THAT IS WHAT THIS METHOD WILL DO
  - STEPS
    - Add the join fetch query to our repository, this will do it all in one step with a single query
    - Just use the new method on the repository

Instructor Repository
  - notice the Query 
```java
public interface InstructorRepository extends JpaRepository<Instructor, Integer> {
    @Query("SELECT i FROM Instructor i " +
            "JOIN FETCH i.courses " +
            "WHERE i.id = ?1")
   public Instructor findInstructorByIdJoinFetch(int id);

```

Use in a method
```java
// get the instructor with the courses loaded thanks to the method we defined above
Instructor instructor = instructorService.getInstructorRepository().findInstructorByIdJoinFetch(instructor_id);

if(instructor == null){
  System.out.println("no instructor with id: " + instructor_id + " was found....");
}
else{
  for(var course : instructor.getCourses()) {
    System.out.println(course);
  }
}
```

We have options now!!
  - If you only need the instructor with no courses loaded
    - `InstructorRepository.findInstructorById(...)`
  - If you need the courses along with the instructor
    - `InstructorRepository.findInstructorByIdJoinFetch(...)`


### Lazy loading error "Hibernate could not initialize proxy – no Session"
  - [error fix and explaination](https://www.baeldung.com/hibernate-initialize-proxy-exception)
  - If you setup lazy loading you could get this error when trying to access the object or the object that is setup to be lazy loaded on the object
  - Access to a lazy-loaded object outside of the context of an open Hibernate session will result in this exception

## Uni-Directional , Bi-Directional
  Uni-Directional
  - ![alt-text](/2023-10-13-udemy-spring-boot-course-section-9-jpa-hibernate-advanced-mappings/uni-directional.png)
    - We retrieve the instructor detail only through the instructor
    - we can't retrieve the instructor through the instructor detail
  
  Bi-Directional
  - ![alt-text](/2023-10-13-udemy-spring-boot-course-section-9-jpa-hibernate-advanced-mappings/bi-directional.png)
  - we can get the instructor detail through the instructor
  - we can get the instructor through the instructor detail

How to make to make a bi-directional relationship
  - we want to make it so we can access the instructor from the instructor detail

```java
// making the relationship bi-directional
// the 'mappedBy' refers to the instructorDetail property in the instructor class
@OneToOne(mappedBy = "instructorDetail")
private Instructor instructor;
```
  - This code is added to the InstructorDetail class
  - mappedBy refers to the instructorDetail variable in the Instructor class

 
# Association Mappings
  - In the database we will have multiple tables and relationships between tables
    - We will need these advanced mappings to describe this in hibernate
  
| Annotation                |
| :------------------------ |
| One-to-One                |
| One-to-Many , Many-to-One |
| Many-to-Many              |


## One-to-One
  - ![alt-text](/2023-10-13-udemy-spring-boot-course-section-9-jpa-hibernate-advanced-mappings/one-to-one.png)
  - [entity table docs for one-to-one](https://www.baeldung.com/jpa-one-to-one)

## One-to-Many
  - ![alt-text](/2023-10-13-udemy-spring-boot-course-section-9-jpa-hibernate-advanced-mappings/one-to-many.png)

## Many-to-Many
  - ![alt-text](/2023-10-13-udemy-spring-boot-course-section-9-jpa-hibernate-advanced-mappings/many-to-many.png)


# @JoinColumn explained
  - ![alt-text](/2023-10-13-udemy-spring-boot-course-section-9-jpa-hibernate-advanced-mappings/how_join_column_works.png)
    - the name in parentheseis is the name of the column name in the given table. This column name acts as the foreign key into the other table, in this case instructor

# mappedBy
  - ![alt-text](/2023-10-13-udemy-spring-boot-course-section-9-jpa-hibernate-advanced-mappings/how_join_column_works.png)
  - `@OneToMany(mapedBy="instructor")` tells spring to look at instructor variable in the  other class that uses `@Joincolumn(name="instructor_id")`

Instructor class
```java
public class Instructor {
  // one instructor can have multiple courses
  // mapped on the instructor variable in the Course class
  @OneToMany(mappedby="instructor", cascade = {CascadeType.PERSIST, CascadeType.DETACH, CascadeType.MERGE, CascadeType.REFRESH})
  private List<Course> courses;
}
```

Course class
```java
public class Course {
  // multiple courses can be mapped to a single instructor
  @ManyToOne
  // Join the instructor table on the column name "instructor_id"
  @JoinColumn(name="instructor_id")
  private Instructor instructor;
}
```

# Examples
  - ![alt-text](/2023-10-13-udemy-spring-boot-course-section-9-jpa-hibernate-advanced-mappings/goal.png)

## Instructor / instructor detail examle
Code to create the database schema
```sql
DROP SCHEMA IF EXISTS `hb-01-one-to-one-uni`;

CREATE SCHEMA `hb-01-one-to-one-uni`;

use `hb-01-one-to-one-uni`;

SET FOREIGN_KEY_CHECKS = 0;

CREATE TABLE `instructor_detail` (
  `id` int NOT NULL AUTO_INCREMENT,
  `youtube_channel` varchar(128) DEFAULT NULL,
  `hobby` varchar(45) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=1 DEFAULT CHARSET=latin1;


CREATE TABLE `instructor` (
  `id` int NOT NULL AUTO_INCREMENT,
  `first_name` varchar(45) DEFAULT NULL,
  `last_name` varchar(45) DEFAULT NULL,
  `email` varchar(45) DEFAULT NULL,
  `instructor_detail_id` int DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `FK_DETAIL_idx` (`instructor_detail_id`),
  CONSTRAINT `FK_DETAIL` FOREIGN KEY (`instructor_detail_id`) REFERENCES `instructor_detail` (`id`) ON DELETE NO ACTION ON UPDATE NO ACTION
) ENGINE=InnoDB AUTO_INCREMENT=1 DEFAULT CHARSET=latin1;

SET FOREIGN_KEY_CHECKS = 1;
```

Instructor Detail entity table
  - nothing to really pay attention to here, normal jpa stuff we have seen before

```java
@Entity
@Table(name = "instructor_detail")
public class InstructorDetail {
    // fields
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "id")
    private int id;

    @Column(name = "youtube_channel")
    private String youtubeChannel;

    @Column(name = "hobby")
    private String hobby;

    // constructors
    public InstructorDetail() {
    }
    public InstructorDetail(String youtubeChannel, String hobby) {
        this.youtubeChannel = youtubeChannel;
        this.hobby = hobby;
    }

    // tostring
    @Override
    public String toString() {
        return "InstructorDetail{" +
                "id=" + id +
                ", youtubeChannel='" + youtubeChannel + '\'' +
                ", hobby='" + hobby + '\'' +
                '}';
    }

    // getter / setter methods


    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getYoutubeChannel() {
        return youtubeChannel;
    }

    public void setYoutubeChannel(String youtubeChannel) {
        this.youtubeChannel = youtubeChannel;
    }

    public String getHobby() {
        return hobby;
    }

    public void setHobby(String hobby) {
        this.hobby = hobby;
    }
}

```

Instructor entity table
  - so whenever there is a foreign key relationship the code to explain that goes in the dependent entity table
  - ex. since instructor has a foreign key that points to instructor detail table we make it known in this entity table
```java
@Entity
@Table(name = "instructor")
public class Instructor {
    // field
    @Id
    @Column(name = "id")
    private int id;

    @Column(name = "first_name")
    private String firstName;

    @Column(name = "last_name")
    private String lastName;

    @Column(name = "email")
    private String email;

    // cannot use otherwise will get an error at runtime
    // @Column(name = "instructor_detail_id")

    @OneToOne(cascade = CascadeType.ALL)
    @JoinColumn(name = "instructor_detail_id")
    private InstructorDetail instructorDetail;

    // constructor

    public Instructor() {
    }

    public Instructor(String firstName, String lastName, String email) {
        this.firstName = firstName;
        this.lastName = lastName;
        this.email = email;
    }

    // tostring
    @Override
    public String toString() {
        return "Instructor{" +
                "id=" + id +
                ", firstName='" + firstName + '\'' +
                ", lastName='" + lastName + '\'' +
                ", email='" + email + '\'' +
                ", instructorDetail=" + instructorDetail +
                '}';
    }

    // getters and setters
    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getFirstName() {
        return firstName;
    }

    public void setFirstName(String firstName) {
        this.firstName = firstName;
    }

    public String getLastName() {
        return lastName;
    }

    public void setLastName(String lastName) {
        this.lastName = lastName;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public InstructorDetail getInstructorDetailId() {
        return instructorDetail;
    }

    public void setInstructorDetailId(InstructorDetail instructorDetailId) {
        this.instructorDetail = instructorDetailId;
    }
}
```


## Instructor Course example
  - ![alt-text](/2023-10-13-udemy-spring-boot-course-section-9-jpa-hibernate-advanced-mappings/instructor_course.png)




## Adding custom method when extending JpaRepository
  - [stack overflow](https://stackoverflow.com/questions/11880924/how-to-add-custom-method-to-spring-data-jpa)
  - You want to add a custom method when extending the JpaRepository
  - Steps
    - place the method signature in the interface when extending JpaRepository
    - create a class with the @Component annotation. name must be the interface + Impl
    - define the method in the class..

Extending from the JpaRepository and defining the custom method
```java
@Repository
public interface InstructorDetailRepository extends JpaRepository<InstructorDetail, Integer> {
    // custom method
    public void RemoveDetailKeepInstructor(int id);
}
```

Class with @Annotation and the method defined
```java
@Component
public class InstructorDetailRepositoryImpl {
    @PersistenceContext
    private EntityManager entityManager;

    @SuppressWarnings("unused")
    @Transactional
    public void RemoveDetailKeepInstructor(int id) {
        // finds the instructor detail by the id
        InstructorDetail instructorDetail = entityManager.find(InstructorDetail.class, id);

        // break the bi-directional link
        instructorDetail.getInstructor().setInstructorDetailId(null);

        // remove the instructor detail
        entityManager.remove(instructorDetail);
    }
}
```

# Many to Many implementation
  - In our example we have a **course**, **student**, and **course_student** table
  - the **course_student** is our **join table**
  - more on the inverse
    - ![alt-text](/2023-10-13-udemy-spring-boot-course-section-9-jpa-hibernate-advanced-mappings/inverse.png)
  - this is how we would handle it in our code


Student Entity class
```java
@Entity
public class Student {
  // ...

  // field declaration for the courses associated with a student
  @ManyToMany
  @JoinTable(
          name = "course_student", // name of the join table
          joinColumns = @JoinColumn(name = "student_id"), // name of the column referring to this table
          inverseJoinColumns = @JoinColumn(name="course_id") // name of the other column referring to the courses table
  )
  private List<Course> courses;
}
```

Course Entity class
```java
@Entity
public class Course {
  // ...
  // field declaration for the students associated with a course
  @ManyToMany
  @JoinTable(
          name = "course_student",
          joinColumns = @JoinColumn(name = "course_id"),
          inverseJoinColumns = @JoinColumn(name = "student_id")
  )
  private List<Student> students;

  
  // method for convenience to add students to the list
  public void addStudent(Student student) {
    if(this.students == null) {
        this.students = new ArrayList<>();
    }
    this.students.add(student);
  }
}
```

Repository for course
```java
public interface CourseRepository extends JpaRepository<Course, Integer> {
    // other implementation

    @Query(value = "SELECT c FROM Course c LEFT JOIN FETCH c.students WHERE c.id=?1")
    Course findCoursesLoadStudents(int courseId);
}
```

Method implementing this
  - Read the comment above `course.addStudent(student);`
  - this method is adding a new student to an existing course
  - this is achieved by adding a new student to the students list in the Course class.
    - saving will cascade to the Student causing a new entry into the Student table as well as an entry into the join table course_student

```java
private void addNewStudent(InstructorServiceImpl instructorService) {
  // get the course id to add the student to
  System.out.print("course id: ");
  int courseId = scanner.nextInt();scanner.nextLine();

  // get the course from the db, loads the students into the students list
  Course course = instructorService.getCourseRepository().findCoursesLoadStudents(courseId);

  if(course == null) {
    System.out.println("unable to find course with id: " + courseId);
    return;
  }

  // assemble the new student
  System.out.print("first name: ");
  String firstName = scanner.nextLine();
  System.out.print("last name: ");
  String lastName = scanner.nextLine();
  String email = "%s.%s@gmail.com".formatted(firstName, lastName);
  Student student = new Student(firstName, lastName, email);

  // WE ONLY NEED TO ADD ONE WAY. MEANING WE DONT HAVE TO ADD THE COURSE TO THE STUDENT OBJECT.
  // THIS IS BECAUSE WHEN WE ADD TO ONE SIDE, IN THIS CASE ADDING A STUDENT TO THE COURSE ASSOCIATION. IT WILL 
  // ... WRITE INTO THE JOIN TABLE
  // .. IF YOU TRIED TO ADD THE OTHER WAY THAT WOULD CAUSE DUPLICATE ENTRIES INTO THE JOIN TABLE WHICH IS BAD!!
  // student.addCourse(course);

  // add student
  course.addStudent(student);

  // persists in the db
  instructorService.getCourseRepository().save(course);

}

```



  