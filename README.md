CREATE TABLE Product (
    id INT PRIMARY KEY,
    name VARCHAR(255),
    price_per_unit DOUBLE,
    active_for_sell BOOLEAN
);
import java.sql.*;

public class ProductListing {
    public static void main(String[] args) {
        String jdbcUrl = "jdbc:mysql://localhost:3306/my_database";
        String username = "root";
        String password = "password";
        try (Connection connection = DriverManager.getConnection(jdbcUrl, username, password);
             Statement statement = connection.createStatement();
             ResultSet resultSet = statement.executeQuery("SELECT id, name, price_per_unit, active_for_sell FROM Product")) {

  // Print header
            System.out.println("Product Listing:");
            System.out.println("---------------------------");

  // Iterate through result set and print each product
            while (resultSet.next()) {
                int id = resultSet.getInt("id");
                String name = resultSet.getString("name");
                double pricePerUnit = resultSet.getDouble("price_per_unit");
                boolean activeForSell = resultSet.getBoolean("active_for_sell");

  // Print product details
                System.out.println("ID: " + id);
                System.out.println("Name: " + name);
                System.out.println("Price per Unit: " + pricePerUnit);
                System.out.println("Active for Sell: " + activeForSell);
                System.out.println("---------------------------");
            }

  } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
