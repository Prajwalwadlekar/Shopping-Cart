import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;
import java.util.Scanner;

// Product Class
class Product {
    private String id;
    private String name;
    private double price;
    private int quantity;

    public Product(String id, String name, double price, int quantity) {
        this.id = id;
        this.name = name;
        this.price = price;
        this.quantity = quantity;
    }

    public String getId() {
        return id;
    }

    public String getName() {
        return name;
    }

    public double getPrice() {
        return price;
    }

    public int getQuantity() {
        return quantity;
    }

    public void setQuantity(int quantity) {
        this.quantity = quantity;
    }
}

// CartItem Class
class CartItem {
    private Product product;
    private int quantity;

    public CartItem(Product product, int quantity) {
        this.product = product;
        this.quantity = quantity;
    }

    public Product getProduct() {
        return product;
    }

    public int getQuantity() {
        return quantity;
    }

    public void setQuantity(int quantity) {
        this.quantity = quantity;
    }

    public double getTotalPrice() {
        return product.getPrice() * quantity;
    }
}

// ShoppingCart Class
class ShoppingCart {
    List<CartItem> items;

    public ShoppingCart() {
        items = new ArrayList<>();
    }

    public void addItem(Product product, int quantity) {
        for (CartItem item : items) {
            if (item.getProduct().getId().equals(product.getId())) {
                item.setQuantity(item.getQuantity() + quantity);
                return;
            }
        }
        items.add(new CartItem(product, quantity));
    }

    public void removeItem(String productId) {
        items.removeIf(item -> item.getProduct().getId().equals(productId));
    }

    public double getTotal() {
        double total = 0;
        for (CartItem item : items) {
            total += item.getTotalPrice();
        }
        return total;
    }

    public void displayCart() {
        if (items.isEmpty()) {
            System.out.println("Your cart is empty.");
            return;
        }
        for (CartItem item : items) {
            System.out.println("Product: " + item.getProduct().getName() + ", Quantity: " + item.getQuantity() + ", Total Price: INR " + item.getTotalPrice());
        }
        System.out.println("Cart Total: INR " + getTotal());
    }
}

// User Class
class User {
    private String id;
    private String name;
    private ShoppingCart cart;

    public User(String id, String name) {
        this.id = id;
        this.name = name;
        this.cart = new ShoppingCart();
    }

    public String getId() {
        return id;
    }

    public String getName() {
        return name;
    }

    public ShoppingCart getCart() {
        return cart;
    }
}

// Coupon Class
class Coupon {
    private String code;
    private double discountPercentage;

    public Coupon(String code, double discountPercentage) {
        this.code = code;
        this.discountPercentage = discountPercentage;
    }

    public String getCode() {
        return code;
    }

    public double getDiscountPercentage() {
        return discountPercentage;
    }
}

// Order Class
class Order {
    private String orderId;
    private User user;
    private List<CartItem> items;
    private double total;
    private double discount;

    public Order(String orderId, User user, Coupon coupon) {
        this.orderId = orderId;
        this.user = user;
        this.items = new ArrayList<>(user.getCart().items);
        this.total = user.getCart().getTotal();
        if (coupon != null) {
            this.discount = (total * coupon.getDiscountPercentage()) / 100;
            this.total -= discount;
        } else {
            this.discount = 0;
        }
    }

    public String getOrderId() {
        return orderId;
    }

    public User getUser() {
        return user;
    }

    public List<CartItem> getItems() {
        return items;
    }

    public double getTotal() {
        return total;
    }

    public double getDiscount() {
        return discount;
    }
}

// Store Class
class Store {
    private Map<String, Product> products;
    private Map<String, Coupon> coupons;

    public Store() {
        products = new HashMap<>();
        coupons = new HashMap<>();
    }

    public void addProduct(Product product) {
        products.put(product.getId(), product);
    }

    public Product getProduct(String productId) {
        return products.get(productId);
    }

    public void displayProducts() {
        System.out.println("\nAvailable Products:");
        for (Product product : products.values()) {
            System.out.println("ID: " + product.getId() + ", Name: " + product.getName() + ", Price: INR " + product.getPrice() + ", Quantity: " + product.getQuantity());
        }
    }

    public void addCoupon(Coupon coupon) {
        coupons.put(coupon.getCode(), coupon);
    }

    public Coupon getCoupon(String code) {
        return coupons.get(code);
    }
}

// Main Class
public class Main {
    public static void main(String[] args) {
        Store store = new Store();

        // Adding Products
        store.addProduct(new Product("1", "Laptop", 69999, 20));
        store.addProduct(new Product("2", "Phone", 49999, 20));
        store.addProduct(new Product("3", "Headphones", 999, 30));
        store.addProduct(new Product("4", "Television", 99999, 30));

        // Adding Coupons
        store.addCoupon(new Coupon("DISCOUNT10", 10)); // 10% discount
        store.addCoupon(new Coupon("DISCOUNT20", 20)); // 20% discount

        User user = new User("1", "Liang");

        Scanner scanner = new Scanner(System.in);
        boolean running = true;
        while (running) {
            System.out.println("\nWelcome to the online store!");
            System.out.println("1. View Products");
            System.out.println("2. Add to Cart");
            System.out.println("3. View Cart");
            System.out.println("4. Checkout");
            System.out.println("5. Exit");
            System.out.print("Enter your choice: ");
            String choice = scanner.nextLine();

            switch (choice) {
                case "1":
                    store.displayProducts();
                    break;
                case "2":
                    store.displayProducts();
                    System.out.print("Enter product ID: ");
                    String productId = scanner.nextLine();
                    System.out.print("Enter quantity: ");
                    int quantity = Integer.parseInt(scanner.nextLine());
                    Product product = store.getProduct(productId);
                    if (product != null && product.getQuantity() >= quantity) {
                        user.getCart().addItem(product, quantity);
                        product.setQuantity(product.getQuantity() - quantity);
                        System.out.println("Product added to cart.");
                    } else {
                        System.out.println("Product not available or insufficient quantity.");
                    }
                    break;
                case "3":
                    user.getCart().displayCart();
                    break;
                case "4":
                    if (user.getCart().items.isEmpty()) {
                        System.out.println("Your cart is empty. Add items to your cart before checking out.");
                    } else {
                        System.out.print("Do you have a coupon code? (yes/no): ");
                        String couponResponse = scanner.nextLine();
                        Coupon coupon = null;
                        if (couponResponse.equalsIgnoreCase("yes")) {
                            System.out.print("Enter coupon code: ");
                            String couponCode = scanner.nextLine();
                            coupon = store.getCoupon(couponCode);
                            if (coupon == null) {
                                System.out.println("Invalid coupon code. Proceeding without discount.");
                            } else {
                                System.out.println("Coupon applied: " + coupon.getDiscountPercentage() + "% off.");
                            }
                        }

                        Order order = new Order("ORD1", user, coupon);
                        System.out.println("Order placed successfully!");
                        System.out.println("Order ID: " + order.getOrderId());
                        if (coupon != null) {
                            System.out.println("Discount Applied: INR " + order.getDiscount());
                        }
                        System.out.println("Total after discount (if any): INR " + order.getTotal());
                        user.getCart().items.clear();
                    }
                    break;
                case "5":
                    System.out.println("Thank you for shopping with us!");
                    running = false;
                    break;
                default:
                    System.out.println("Invalid choice. Please try again.");
            }
        }
        scanner.close();
    }
}
