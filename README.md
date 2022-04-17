# marksCalculates
package com.nt.dao;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.PreparedStatement;
import javax.naming.InitialContext;
import javax.sql.DataSource;
import com.nt.VO.StudentVO;
public class StudentDAO {
private static final String STUDENT_INSERT_QUEARY_="INSERT INTO STUDENT_TABLE VALUES(?,?,?,?,?)";
private static final String STUDENT_INSERT_QUEARY = null;
public int insert(StudentVO vo) {
	//create variable below 
	InitialContext ic=null;
	DataSource ds=null;
	Connection con=null;
	PreparedStatement ps=null;
	int result=0;
	try {
		//create InitialContext
		ic=new InitialContext();
		//get datasource object throught lookup operation
		ds=(DataSource)ic.lookup("Dsjndi");
		//get Connection JDBC object 
		con=ds.getConnection();
		//create PreparedStatement object 
		ps=con.prepareStatement(STUDENT_INSERT_QUEARY);
		//set values as queary params 
		//ps.setInt(1,vo.getSno());
		//ps.setString(2,vo.getSname());
		//ps.setInt(3,vo.getTotal());
		//ps.setFloat(4,vo.getAvg());
		//ps.setString(5,vo.getResult());
		//excuate queary 
		result=ps.executeUpdate();
	}catch(Exception e) {
		e.printStackTrace();
	}//end of the catch block
	
	finally {
		try {
			if(ps!=null)
				ps.close();
		}catch(SQLException e) {
			e.printStackTrace();
		}//end of teh catch block
		try {
			if(con!=null)
				con.close();
		}catch(SQLException e) {
			e.printStackTrace();
		}//end of the catch block
		
	}//end of the finally block
	return result;
}//end method()
}//end of the class
