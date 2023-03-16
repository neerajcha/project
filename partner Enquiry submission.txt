<%@ page contentType="text/html; charset=UTF-8" language="java" %>
<%@ page import="java.sql.*" %>
<%
    String fullName = request.getParameter("fullname");
    String mobno = request.getParameter("mobno");
    String email = request.getParameter("email");
    String resiPinCode = request.getParameter("resipincode");
    String shops = request.getParameter("shops");

    try {
        
        Class.forName("com.mysql.jdbc.Driver");
        
        // Connect to the database
        String url = "jdbc:mysql://localhost:3306/mylaundrywala"; 
        String username = "root"; 
        String password = "root"; 
        Connection conn = DriverManager.getConnection(url, username, password);
        
        
        String sql = "INSERT INTO penquiry (fullname, mobno, email, resipincode, shops) VALUES (?, ?, ?, ?, ?)";
        PreparedStatement statement = conn.prepareStatement(sql);
        statement.setString(1, fullName);
        statement.setString(2, mobno);
        statement.setString(3, email);
        statement.setString(4, resiPinCode);
        statement.setString(5, shops);
        
        
        int rowsInserted = statement.executeUpdate();
        if (rowsInserted > 0) {
            out.println("Data inserted successfully!");
        } else {
            out.println("Error inserting data");
        }
        
        conn.close();
        
    } catch (ClassNotFoundException | SQLException e) {
        out.println("Error: " + e.getMessage());
    }
%>