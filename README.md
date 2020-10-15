# CCTech-Software-Developer-Hiring-Challenge-program
Program 1 : Check if the given point lies inside or outside a polygon?

package program1;

import program1.polygon.Point;

public class polygon {
	
	static int range=10000;
	static class Point  
    { 
		double x_coordinate; 
		double y_coordinate; 
        public Point(double x_coordinate, double y_coordinate) 
        { 
            this.x_coordinate = x_coordinate; 
            this.y_coordinate = y_coordinate; 
        } 
    }; 
    
    static boolean onLine(Point a, Point p, Point b)  
    { 
        if (p.x_coordinate <= Math.max(a.x_coordinate, b.x_coordinate) && 
            p.x_coordinate >= Math.min(a.x_coordinate, b.x_coordinate) && 
            p.y_coordinate <= Math.max(a.y_coordinate, b.y_coordinate) && 
            p.y_coordinate >= Math.min(a.y_coordinate, b.y_coordinate)) 
        { 
            return true; 
        } 
        return false; 
    } 
    
    static double direction(Point a, Point p, Point b)  
    { 
    	double val = (p.y_coordinate - a.y_coordinate) * (b.x_coordinate - p.x_coordinate) 
                - (p.x_coordinate - a.x_coordinate) * (b.y_coordinate - p.y_coordinate); 
  
        if (val == 0)  
        { 
            return 0; 
        } 
        else if(val < 0)
            return 2;          
            return 1;      
    }    
	public static boolean intersect(Point a1, Point b1,  
		            Point a2, Point b2)  
		{ 
		//dircetion case
		double case1 = direction(a1, b1, a2); 
		double case2 = direction(a1, b1, b2); 
		double case3 = direction(a2, b2, a1); 
		double case4 = direction(a2, b2, b1); 
		
		if (case1 != case2 && case3 != case4) 
		{ 
		return true; 
		} 
				
		if (case1 == 0 && onLine(a1, a2, b1))  
		{ 
		return true; 
		} 
				
		if (case2 == 0 && onLine(a1, b2, b1))  
		{ 
		return true; 
		} 
				
		if (case3 == 0 && onLine(a2, a1, b2)) 
		{ 
		return true; 
		} 
		
		if (case4 == 0 && onLine(a2, b1, b2)) 
		{ 
		return true; 
		} 
		
		return false;  
	} 
	
   static boolean inside(Point polygon[], int poly_limit, Point p) 
          {      
             if (poly_limit < 3)  
              { 
                return false; 
              } 
  
         Point extreme = new Point(range, p.y_coordinate); 
  
          int count = 0, i = 0; 
        do 
        { 
            int next = (i + 1) % poly_limit; 
  
            if (intersect(polygon[i], polygon[next], p, extreme))  
            { 
                if (direction(polygon[i], p, polygon[next]) == 0) 
                { 
                    return  onLine(polygon[i], p, 
                                     polygon[next]); 
                } 
  
                count++; 
            } 
            i = next; 
        } while (i != 0); 
  
        return (count % 2 == 1); 
    } 	
	public static void main(String[] args) {
		Point polygon_test[] = {new Point(0, 1), 
                new Point(8, 3),  
                new Point(8, 8),  
                new Point(1, 5)}; 
		
		//int poly_limit = polygon_test.length;
		int poly_limit = 4;
		 Point p = new Point(3, 5); 
		 System.out.println("Case1 polygon"); 
		 if (inside( polygon_test, poly_limit, p)) 
	        { 
	            System.out.println("True-->Inside the polygon"); 
	        }  
	        else 
	        { 
	            System.out.println("False-->Outsie the polygon"); 
	        } 
		 
		 Point polygon_test2[] = {new Point(-3, 2), 
	                new Point(-2, -0.8),  
	                new Point(0, 1.2),  
	                new Point(2.2, 0), new Point(2.4, 5)}; 			
			
		      poly_limit = polygon_test.length;
			  p = new Point(0, 0); 
			  System.out.println("Case2 polygon"); 
			 if (inside( polygon_test2, poly_limit, p)) 
		        { 
		            System.out.println("True-->Inside the polygon"); 
		        }  
		        else 
		        { 
		            System.out.println("False-->Outsie the polygon"); 
		        } 

	}
		
}

