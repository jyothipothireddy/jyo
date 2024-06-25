import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.PreparedStatement;
import java.util.Scanner;

public class LabExpt3 {

  public static void main(String[] args) {
    // TODO Auto-generated method stub
    Connection conn;
    PreparedStatement ps;
    ResultSet rs;
    try {
      Class.forName("com.mysql.jdbc.Driver");
      conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/VVIT", "root", "");
      Scanner sc = new Scanner(System.in);
      System.out.println("The choices are: " + "\t1.Add \t2.Delete\t3.Modify\t4.Retrieve");
      int choice = sc.nextInt();
      switch (choice) {
        case 1:
          ps = conn.prepareStatement("insert into Studen1 values(?,?);");
          System.out.println("Enter student number and name:");
          int no = sc.nextInt();
          String str = sc.next();
          ps.setInt(1, no);
          ps.setString(2, str);
          ps.executeUpdate();
          System.out.println("Inserted succesfully");
          break;
        case 2:
          ps = conn.prepareStatement("delete from Studen1 where rool_no=?");
          System.out.println("Enter roll number:");
          int roll = sc.nextInt();
          ps.setInt(1, roll);
          ps.executeUpdate();
          System.out.println("Deleted succesfully");
          break;
        case 3:
          ps = conn.prepareStatement("update Studen1 set name=? where rool_no=?");
          System.out.println("Enter existing roll number and new name:");
          no = sc.nextInt();
          str = sc.next();
          ps.setString(1, str);
          ps.setInt(2, no);
          ps.executeUpdate();
          System.out.println("Updated succesfully");
          break;
        case 4:
          ps = conn.prepareStatement("select * from Studen1;");
          rs = ps.executeQuery();
          while (rs.next()) {
            System.out.println(rs.getInt(1) + "\t" + rs.getString(2));
          }
          break;
        default:
          System.out.println("Invalid choice");
          System.exit(0);
      }
      conn.close();
    } catch (ClassNotFoundException e) {
      e.printStackTrace();
    } catch (SQLException e) {
      e.printStackTrace();
    }
}
}
