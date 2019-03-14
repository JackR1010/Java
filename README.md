# Java
Java Code
import java.io.*;
import java.util.*;
import java.util.regex.Matcher;
import java.util.regex.Pattern;


public class cookie {
    static int i = 0;
    static Vector<Double> vec;
    static double target=0;
    static double fRate = 0;
    static double fCost = 0;
    
    public static double fun(double prevFarmBuyTimes, double rate){
        if(i==0){
            vec.add(target/rate);
        }
        double farmTime = prevFarmBuyTimes+fCost/rate;
        rate+=fRate;
        double WaitingTime = target/rate;
        double projection = farmTime+WaitingTime;
        vec.add(projection);
        i++;
        if(vec.elementAt(i-1)>vec.elementAt(i)){
            return fun(farmTime, rate);
        }
        else
        {
            return vec.elementAt(i-1);
        }
    }
    
    public static void main(String[] args) throws Exception{
        BufferedReader br = new BufferedReader(new FileReader("d:\\B-large-practice.in"));
        BufferedWriter bw = new BufferedWriter(new FileWriter("d:\\result.txt"));
        
        int ncases = Integer.parseInt(br.readLine());
        int index = 1;
        while(index<=ncases){
            
            Pattern p = Pattern.compile("\\d+.\\d+");
            Matcher m = p.matcher(br.readLine());
            
            if (m.find())
            fCost = Double.parseDouble(m.group());
            
            if (m.find())
            fRate = Double.parseDouble(m.group());
            
            if (m.find())
            target = Double.parseDouble(m.group());
            
            
            //LOGIC STARTS HERE
             vec = new Vector<Double>();
             i=0;
             double time = fun(0,2);
             
             bw.write("Case #"+index+": "+time);
             bw.newLine();
             bw.flush();
             System.out.println(time);
             index++;
        }    
    }    
}
