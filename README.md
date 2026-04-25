# P2-oop
import java.util.*;

interface Passable {
    boolean isPass();
}

abstract class Student implements Passable {
    private String name;
    private double mark;

    public Student(String name, double mark) {
        this.name = name;
        setMark(mark);
    }

    public String getName() {
        return name;
    }

    public double getMark() {
        return mark;
    }

    public void setMark(double mark) {
        if (mark < 0 || mark > 100) {
            throw new IllegalArgumentException("Invalid mark");
        }
        this.mark = mark;
    }

    public abstract double getPassMark();
}

class UndergraduateStudent extends Student {
    public UndergraduateStudent(String name, double mark) {
        super(name, mark);
    }

    public double getPassMark() {
        return 60;
    }

    public boolean isPass() {
        return getMark() >= getPassMark();
    }
}

class GraduateStudent extends Student {
    public GraduateStudent(String name, double mark) {
        super(name, mark);
    }

    public double getPassMark() {
        return 80;
    }

    public boolean isPass() {
        return getMark() >= getPassMark();
    }
}

class StudentSystem {
    private ArrayList<Student> students = new ArrayList<>();

    public void addStudent(Student s) {
        students.add(s);
    }

    public void updateMark(String name, double newMark) {
        for (Student s : students) {
            if (s.getName().equalsIgnoreCase(name)) {
                try {
                    s.setMark(newMark);
                } catch (Exception e) {
                    System.out.println("Error: " + e.getMessage());
                }
            }
        }
    }

    public void printAll() {
        for (Student s : students) {
            System.out.println(
                s.getName() + " - " + s.getMark() +
                " - " + (s.isPass() ? "Pass" : "Fail")
            );
        }
    }
}

public class Main {
    public static void main(String[] args) {
        StudentSystem system = new StudentSystem();

        system.addStudent(new UndergraduateStudent("Ali", 55));
        system.addStudent(new GraduateStudent("Sara", 75));

        system.printAll();

        system.updateMark("Ali", 65);

        System.out.println("After update:");
        system.printAll();
    }
}

