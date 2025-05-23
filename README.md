import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

class Car {
    private String brand;
    private String model;
    private String color;
    private int year;
    private double pricePerHour;

    public Car(String brand, String model, String color, int year, double pricePerHour) {
        this.brand = brand;
        this.model = model;
        this.color = color;
        this.year = year;
        this.pricePerHour = pricePerHour;
    }

    @Override
    public String toString() {
        return "Brand: " + brand + ", Model: " + model + ", Color: " + color + ", Year: " + year + ", Price per Hour: $" + pricePerHour;
    }
}

class Admin {
    private String firstName;
    private String lastName;
    private String email;
    private String phone;
    private String password;

    public Admin(String firstName, String lastName, String email, String phone, String password) {
        this.firstName = firstName;
        this.lastName = lastName;
        this.email = email;
        this.phone = phone;
        this.password = password;
    }

    @Override
    public String toString() {
        return "Admin: " + firstName + " " + lastName + ", Email: " + email + ", Phone: " + phone;
    }
}

class User {
    public String firstName;
    public String lastName;
    public String email;
    public String phone;
    public String password;

    public User(String firstName, String lastName, String email, String phone, String password) {
        this.firstName = firstName;
        this.lastName = lastName;
        this.email = email;
        this.phone = phone;
        this.password = password;
    }

    public String getEmail() {
        return email;
    }

    public String getPassword() {
        return password;
    }

    @Override
    public String toString() {
        return "User: " + firstName + " " + lastName + ", Email: " + email + ", Phone: " + phone;
    }
}

public class CarRentalSystem {
    private List<Car> cars;
    private List<Admin> admins;
    private List<User> users;
    private User currentUser;

    public CarRentalSystem() {
        cars = new ArrayList<>();
        admins = new ArrayList<>();
        users = new ArrayList<>();
    }

    public void addCar(String brand, String model, String color, int year, double pricePerHour) {
        Car car = new Car(brand, model, color, year, pricePerHour);
        cars.add(car);
        System.out.println("Car added successfully!");
    }

    public void viewCars() {
        if (cars.isEmpty()) {
            System.out.println("No cars available.");
        } else {
            for (Car car : cars) {
                System.out.println(car);
            }
        }
    }

    public void showRents() {
        // Implementation to show rents
        System.out.println("Showing rents...");
    }

    public void showUserRent(User user) {
        // Implementation to show specific user's rent
        System.out.println("Showing rent details for user: " + user);
    }

    public void editUserData(User user) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Editing user data for: " + user);
        System.out.print("Enter new first name: ");
        user.firstName = scanner.nextLine();
        System.out.print("Enter new last name: ");
        user.lastName = scanner.nextLine();
        System.out.print("Enter new email: ");
        user.email = scanner.nextLine();
        System.out.print("Enter new phone: ");
        user.phone = scanner.nextLine();
        System.out.println("User data updated successfully!");
    }

    public void changePassword(User user) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter current password: ");
        String currentPassword = scanner.nextLine();
        if (!user.password.equals(currentPassword)) {
            System.out.println("Incorrect password!");
            return;
        }
        System.out.print("Enter new password: ");
        String newPassword = scanner.nextLine();
        System.out.print("Confirm new password: ");
        String confirmPassword = scanner.nextLine();
        if (!newPassword.equals(confirmPassword)) {
            System.out.println("Passwords do not match!");
            return;
        }
        user.password = newPassword;
        System.out.println("Password changed successfully!");
    }

    public void showAdmins() {
        if (admins.isEmpty()) {
            System.out.println("No admins available.");
        } else {
            System.out.println("Admins:");
            for (Admin admin : admins) {
                System.out.println(admin);
            }
        }
    }

    public void showUsers() {
        if (users.isEmpty()) {
            System.out.println("No users available.");
        } else {
            System.out.println("Users:");
            for (User user : users) {
                System.out.println(user);
            }
        }
    }

    public void loginUser() {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter email: ");
        String email = scanner.nextLine();
        System.out.print("Enter password: ");
        String password = scanner.nextLine();

        for (User user : users) {
            if (user.getEmail().equals(email) && user.getPassword().equals(password)) {
                currentUser = user;
                System.out.println("Login successful!");
                return;
            }
        }
        System.out.println("Invalid email or password.");
    }

    public void registerUser() {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter first name: ");
        String firstName = scanner.nextLine();
        System.out.print("Enter last name: ");
        String lastName = scanner.nextLine();
        System.out.print("Enter email: ");
        String email = scanner.nextLine();
        System.out.print("Enter phone: ");
        String phone = scanner.nextLine();
        System.out.print("Enter password: ");
        String password = scanner.nextLine();

        User newUser = new User(firstName, lastName, email, phone, password);
        users.add(newUser);
        System.out.println("Registration successful!");
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        CarRentalSystem system = new CarRentalSystem();

        while (true) {
            System.out.println("\nCar Rental System Menu:");
            if (system.currentUser == null) {
                System.out.println("1. Register");
                System.out.println("2. Login");
                System.out.println("3. Quit");
                System.out.print("Enter your choice: ");
                int choice = scanner.nextInt();
                scanner.nextLine(); // Consume newline

                switch (choice) {
                    case 1:
                        system.registerUser();
                        break;
                    case 2:
                        system.loginUser();
                        break;
                    case 3:
                        System.out.println("Exiting...");
                        System.exit(0);
                        break;
                    default:
                        System.out.println("Invalid choice!");
                }
            } else {
                System.out.println("1. Add new car");
                System.out.println("2. View cars");
                System.out.println("3. Show rents");
                System.out.println("4. Show my rent");
                System.out.println("5. Edit my data");
                System.out.println("6. Change password");
                System.out.println("7. Show admins");
                System.out.println("8. Show users");
                System.out.println("9. Logout");
                System.out.print("Enter your choice: ");
                int choice = scanner.nextInt();
                scanner.nextLine(); // Consume newline

                switch (choice) {
                    case 1:
                        System.out.print("Enter brand: ");
                        String brand = scanner.nextLine();
                        System.out.print("Enter model: ");
                        String model = scanner.nextLine();
                        System.out.print("Enter color: ");
                        String color = scanner.nextLine();
                        System.out.print("Enter year: ");
                        int year = scanner.nextInt();
                        System.out.print("Enter price per hour: ");
                        double pricePerHour = scanner.nextDouble();
                        scanner.nextLine(); // Consume newline
                        system.addCar(brand, model, color, year, pricePerHour);
                        break;
                    case 2:
                        system.viewCars();
                        break;
                    case 3:
                        system.showRents();
                        break;
                    case 4:
                        system.showUserRent(system.currentUser);
                        break;
                    case 5:
                        system.editUserData(system.currentUser);
                        break;
                    case 6:
                        system.changePassword(system.currentUser);
                        break;
                    case 7:
                        system.showAdmins();
                        break;
                    case 8:
                        system.showUsers();
                        break;
                    case 9:
                        system.currentUser = null;
                        System.out.println("Logged out successfully!");
                        break;
                    default:
                        System.out.println("Invalid choice!");
                }
            }
        }
    }
}


