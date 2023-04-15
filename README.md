# Employee_List_Average_Salary_And_Maximum_Rating

import java.util.ArrayList;

import java.util.Comparator;

import java.util.List;

import java.util.Map;

import java.util.stream.Collectors;

/**
 * We first use the Collectors.groupingBy method to group the employees by their
 
 * department.We then use the Collectors.averagingDouble method to calculate the
 
 * average salary for each department. For maximum rating we use the
 
 * Collectors.collectingAndThen method to first calculate the maximum rating
 
 * using the Collectors.maxBy method and then use the Optional.Map method to
 
 * extract the rating value return a default value of 0 if there are no
 
 * employees in the department.
 * 
 * @author Firoj
 
 * @since 2022-01-05
 
 */
 
public class AccolightEmployeList {

	private String name;
  
	private String department;
  
	private String location;
  
	private double salary;
  
	private int rating;

	public AccolightEmployeList(String name, String department, String location, double salary, int rating) {
  
		super();
    
		this.name = name;
    
		this.department = department;
    
		this.location = location;
    
		this.salary = salary;
    
		this.rating = rating;
    
	}

	public String getName() {
  
		return name;
    
	}

	public void setName(String name) {
  
		this.name = name;
    
	}

	public String getDepartment() {
  
		return department;
    
	}

	public void setDepartment(String department) {
  
		this.department = department;
    
	}

	public String getLocation() {
  
		return location;
    
	}

	public void setLocation(String location) {
  
		this.location = location;
    
	}

	public double getSalary() {
  
		return salary;
    
	}

	public void setSalary(double salary) {
  
		this.salary = salary;
    
	}

	public int getRating() {
  
		return rating;
    
	}

	public void setRating(int rating) {
  
		this.rating = rating;
    
	}

	@Override
  
	public String toString() {
  
		return "Acculightcompany [name=" + name + ", department=" + department + ", location=" + location + ", salary="
    
				+ salary + ", rating=" + rating + "]";
        
	}
  

	public static void main(String[] args) {
  

		List<AccolightEmployeList> emp = new ArrayList<AccolightEmployeList>();// populate employee data
    
		emp.add(new AccolightEmployeList("firoj", "it", "mbd", 1000.50, 4));
    
		emp.add(new AccolightEmployeList("dipu", "hr", "noida", 2000.50, 3));
    
		emp.add(new AccolightEmployeList("tanis", "cs", "delhi", 3000.50, 6));
    
		emp.add(new AccolightEmployeList("husne", "hr", "hyd", 4000.50, 1));

		// Group Employee by department snd calculate average salary and maximum rating.
    
		Map<String, Double> avragesalBydept = emp.stream().collect(Collectors.groupingBy(
    
				AccolightEmployeList::getDepartment, Collectors.averagingDouble(AccolightEmployeList::getSalary)));

		Map<String, Integer> maxRaitingByDepart = emp.stream()
    
				.collect(Collectors.groupingBy(AccolightEmployeList::getDepartment,
        
						Collectors.collectingAndThen(
            
								Collectors.maxBy(Comparator.comparingInt(AccolightEmployeList::getRating)),
                
								max -> max.map(AccolightEmployeList::getRating).orElse(0))));
                
		// Print he result
    
		System.out.println("Avrage Salary by Departement:" + avragesalBydept);
    
		System.out.println("Maximum Rating by department:-" + maxRaitingByDepart);
    
	}


}

Output:-

Avrage Salary by Departement:{cs=3000.5, hr=3000.5, it=1000.5}

Maximum Rating by department:-{cs=6, hr=3, it=4}
