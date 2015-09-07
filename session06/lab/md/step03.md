#Adding a new Class to Expose as the Web Service

Take the following POJO "DonationService" class as a starting point and add the relevant Jersey annotations to expose the class as a service called "api" and then the individual methods to "getall", "get", "insert" and "delete" donations in your mysql database.

As there's a bit of work to do here, below is the completed class, exposed as a web service - just make sure you update the 'URL' to match your username/password settings in XAMPP.

You will however need to create your own <b>Donation</b> class so try and work out what attributes this class should have based on the class below.

~~~java
package com.jumpyjosh.donation;

import java.io.IOException;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.ArrayList;
import java.util.Collections;

import javax.ws.rs.Consumes;
import javax.ws.rs.DELETE;
import javax.ws.rs.GET;
import javax.ws.rs.POST;
import javax.ws.rs.PUT;
import javax.ws.rs.Path;
import javax.ws.rs.PathParam;
import javax.ws.rs.Produces;
import javax.ws.rs.core.MediaType;
import javax.ws.rs.core.Response;

import com.google.gson.Gson;

@Path("/api")
public class DonationService {

	private static Connection conn = null;
	private String driver = "com.mysql.jdbc.Driver";
	// YOU'LL NEED TO SET YOUR OWN USER & PASSWORD VALUES HERE... (REPLACE THE ????'s with your own credentials)
	private String URL = "jdbc:mysql://localhost:3306/donations?user=????&password=????&autoReconnect=true";
	
	private void connectJDBC() throws IOException,SQLException
	{
		try {
			// Load database driver if not already loaded.
			Class.forName(driver);
			System.out.println("Driver Loaded OK");
			// Establish network connection to database.
	
				conn = DriverManager.getConnection(URL);
				System.out.println("Connected");
		
		}
		catch(SQLException sqle) {
			System.out.println("Error connecting: " + sqle);
			sqle.printStackTrace();
			}
		catch(Exception cnfe) {
			System.out.println("Error loading driver: " + cnfe);
			} 
	}
	
	public boolean isConnected()
	{
		if (conn != null)
				return true;
		else
				return false;
	}
	
	public boolean disconnect()
	{
		if (conn != null)
		{
			try {
				conn.close();
			} 
			catch (SQLException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
				return false;
			}			
		}		
		return true;
	}
	  
	@GET
	@Produces({ MediaType.APPLICATION_XML, MediaType.APPLICATION_JSON })
	@Path("/getall")
	public String getAllDonations() throws SQLException, IOException
	  {
	    connectJDBC();     
	    Statement statement = conn.createStatement();
	    String counter = "select count(*) from donation";
	    ResultSet counterSet = statement.executeQuery(counter);
	  
	    int count = 0;
	    if(counterSet.next()) 
	        count = counterSet.getInt(1);
	    String query = "SELECT id, type, amount, user FROM donation";
	    // Send query to database and store results.
	    ResultSet resultSet = statement.executeQuery(query); 
	    ArrayList<Donation> list = new ArrayList<Donation>();
	    
	    while(resultSet.next()){
	      Donation temp = new Donation();
	      temp.id = resultSet.getInt(1);
	      temp.type = resultSet.getString(2);
	      temp.amount = resultSet.getFloat(3);
	      temp.user = resultSet.getString(4);       
	      list.add(temp);
	    }
	    disconnect();  
	    Gson gson = new Gson();
	    String returnList = gson.toJson(list);
	    
	    return returnList;
	  }
	  
	@POST
	@Consumes({MediaType.APPLICATION_XML,MediaType.APPLICATION_JSON})
	@Produces({ MediaType.TEXT_PLAIN})
	@Path("/insert")
	public String insertADonation(Donation d) throws SQLException, IOException
	{
		Response res = null;  
		try {
		connectJDBC();
		
		Statement statement = conn.createStatement();
		String sql = "INSERT INTO donation VALUES(null," + 
		             "'" + d.type + "','" + d.amount + "','" + d.user + "')";
		
//		Gson gson = new Gson();
		
		Boolean result = statement.execute(sql);
		
		res = Response.status(201).entity("OK").build();
	    return res.toString();     
		}
		catch (Exception e)
		{
		res = Response.status(400).entity("FAIL").build();
		return res.toString();
		}
		
		finally{disconnect();}
	}
	
	
	@DELETE
	@Consumes({MediaType.APPLICATION_XML,MediaType.APPLICATION_JSON})
	@Produces({ MediaType.TEXT_PLAIN})
	@Path("/delete/{id}")
	public String deleteADonation(@PathParam("id")int id) throws SQLException, IOException
	{
		
		Response res = null;
		try {
		connectJDBC();
		
		Statement statement = conn.createStatement();
		String sql = "DELETE FROM donation WHERE donation.id = '" + id + "'";
		
		boolean result = statement.execute(sql);
		
		res = Response.status(201).entity("OK").build();
	    return res.toString();     
		}
		catch (Exception e)
		{
		res = Response.status(400).entity("FAIL").build();
		return res.toString();
		}
		
		finally{disconnect();}
	}
	
	@GET
	@Produces({ MediaType.APPLICATION_XML, MediaType.APPLICATION_JSON })
	@Path("/get/{id}")
	public String getADonation(@PathParam("id")int id) throws SQLException, IOException {
		connectJDBC();
		
		Statement statement = conn.createStatement();
		String counter = "select count(*) from donation";
		ResultSet counterSet = statement.executeQuery(counter);
	
		int count = 0;
		if(counterSet.next())	
				count = counterSet.getInt(1);
		String sql = "SELECT * FROM donation WHERE id = '" + id + "'";
		// Send query to database and store results.
		ResultSet resultSet = statement.executeQuery(sql);
	
		Donation temp = new Donation();
		
		while(resultSet.next())
		{
			  temp.id = resultSet.getInt(1);
		      temp.type = resultSet.getString(2);
		      temp.amount = resultSet.getFloat(3);
		      temp.user = resultSet.getString(4);				
		}
		disconnect();
		
		 	Gson gson = new Gson();
		    String returnCoffee = gson.toJson(temp);
	
		return returnCoffee;
	}	
}
~~~

