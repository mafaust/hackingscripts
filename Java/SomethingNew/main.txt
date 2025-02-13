import myapp.controller.UserController;
import myapp.model.User;
import myapp.service.UserService;

public class Main {
    public static void main(String[] args) {
        UserService userService = new UserService();
        UserController userController = new UserController(userService);
        
        userController.createUser("Alice", 25);
        userController.createUser("Bob", 30);
        
        userController.listUsers();
    }
}

// User Model
package myapp.model;

public class User {
    private String name;
    private int age;

    public User(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }

    @Override
    public String toString() {
        return "User{name='" + name + "', age=" + age + "}";
    }
}

// User Service
package myapp.service;

import myapp.model.User;
import java.util.ArrayList;
import java.util.List;

public class UserService {
    private List<User> users = new ArrayList<>();

    public void addUser(String name, int age) {
        users.add(new User(name, age));
    }

    public List<User> getUsers() {
        return users;
    }
}

// User Controller
package myapp.controller;

import myapp.service.UserService;
import myapp.model.User;

public class UserController {
    private UserService userService;

    public UserController(UserService userService) {
        this.userService = userService;
    }

    public void createUser(String name, int age) {
        userService.addUser(name, age);
        System.out.println("User " + name + " created successfully.");
    }

    public void listUsers() {
        System.out.println("Listing users:");
        for (User user : userService.getUsers()) {
            System.out.println(user);
        }
    }
}

// Utility Class
package myapp.util;

import java.text.SimpleDateFormat;
import java.util.Date;

public class DateUtil {
    public static String getCurrentTimestamp() {
        return new SimpleDateFormat("yyyy-MM-dd HH:mm:ss").format(new Date());
    }
}
