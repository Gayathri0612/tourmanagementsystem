import java.util.*;

class Tour {
    public String tourName;
    public double pricePerDay;
    public String offer;
    public String hotelType;

    public Tour(String tourName, double pricePerDay, String offer, String hotelType) {
        this.tourName = tourName;
        this.pricePerDay = pricePerDay;
        this.offer = offer;
        this.hotelType = hotelType;
    }

    public String getTourName() {
        return tourName;
    }

    public double getPrice() {
        return pricePerDay;
    }

    @Override
    public String toString() {
        return tourName + " | ₹" + pricePerDay + "/day | Offer: " + offer + " | Hotel: " + hotelType;
    }
}

class Booking {
    public String customerName;
    public String email;
    public String phone;
    public Tour tour;
    public int days;
    public int people;
    public double totalCost;

    public Booking(String customerName, String email, String phone, Tour tour, int days, int people) {
        this.customerName = customerName;
        this.email = email;
        this.phone = phone;
        this.tour = tour;
        this.days = days;
        this.people = people;
        this.totalCost = tour.getPrice() * days * people;
    }

    @Override
    public String toString() {
        return "\n--- Booking Summary ---\n" +
                "Customer Name: " + customerName +
                "\nEmail: " + email +
                "\nPhone: " + phone +
                "\nTour: " + tour +
                "\nDays Selected: " + days +
                "\nPeople: " + people +
                "\nTotal Cost: ₹" + totalCost;
    }
}

class TourManager {
    private List<Tour> tours = new ArrayList<>();
    private List<Booking> bookings = new ArrayList<>();

    public void addTour(Tour tour) {
        tours.add(tour);
    }

    public List<Tour> getTours() {
        return tours;
    }

    public void listTours() {
        System.out.println("\n--- Available Tours ---");
        for (Tour tour : tours) {
            System.out.println(tour);
        }
    }

    public void addBooking(Booking booking) {
        bookings.add(booking);
    }

    public void listBookings() {
        if (bookings.isEmpty()) {
            System.out.println("No bookings yet.");
        } else {
            for (Booking booking : bookings) {
                System.out.println(booking);
            }
        }
    }
}

public class TourManagementSystem {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        TourManager manager = new TourManager();

        manager.addTour(new Tour("Kerala", 2500, "10% off", "5-Star"));
        manager.addTour(new Tour("Goa", 3000, "Free Breakfast", "4-Star"));
        manager.addTour(new Tour("Manali", 2800, "15% off", "3-Star"));
        manager.addTour(new Tour("Jaipur", 2200, "2 Nights Free", "Heritage"));
        manager.addTour(new Tour("Darjeeling", 2700, "5% off", "4-Star"));
        manager.addTour(new Tour("Rajasthan Desert", 3200, "Camel Ride Free", "Luxury Tent"));
        manager.addTour(new Tour("Kashmir", 3500, "10% off", "5-Star"));
        manager.addTour(new Tour("Andaman", 4000, "Scuba Diving Free", "Beach Resort"));
        manager.addTour(new Tour("Ooty", 2300, "15% off", "3-Star"));
        manager.addTour(new Tour("Mysore", 2100, "Free Dinner", "Heritage"));

        while (true) {
            System.out.println("\n=== Tourism Management System ===");
            System.out.println("1. View Tours");
            System.out.println("2. Book a Tour");
            System.out.println("3. View All Bookings");
            System.out.println("4. Exit");
            System.out.print("Enter choice: ");
            int choice = Integer.parseInt(scanner.nextLine());

            switch (choice) {
                case 1:
                    manager.listTours();
                    break;

                case 2:
                    System.out.print("Enter Your Name: ");
                    String custName = scanner.nextLine();

                    System.out.print("Enter Your Email: ");
                    String custEmail = scanner.nextLine();

                    System.out.print("Enter Your Phone Number: ");
                    String custPhone = scanner.nextLine();

                    System.out.print("Enter Tour Name: ");
                    String tourName = scanner.nextLine();
                    Tour selectedTour = null;
                    for (Tour tour : manager.getTours()) {
                        if (tour.getTourName().equalsIgnoreCase(tourName)) {
                            selectedTour = tour;
                            break;
                        }
                    }

                    if (selectedTour != null) {
                        System.out.print("How many days you want? ");
                        int days = Integer.parseInt(scanner.nextLine());
                        System.out.print("Number of people: ");
                        int people = Integer.parseInt(scanner.nextLine());

                        Booking booking = new Booking(custName, custEmail, custPhone, selectedTour, days, people);
                        manager.addBooking(booking);
                        System.out.println(booking);
                        System.out.println("Booking Successful!");
                    } else {
                        System.out.println("Tour not found!");
                    }
                    break;

                case 3:
                    manager.listBookings();
                    break;

                case 4:
                    System.out.println("Thank you for booking visit again...!!! ");
                    scanner.close();
                    return;

                default:
                    System.out.println("Invalid choice. Please try again.");
            }
        }
    }
}
