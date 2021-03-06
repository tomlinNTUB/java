# J04  讀寫csv檔


## (1) 讀入一個csv檔

```
Java專案
   |__ Main.java
   |__ exams.csv (輸入檔) 
```

### Main.java

```java
import java.io.*;

class Main {
    public static void main(String[] args) throws IOException {
        // 宣告檔案讀取變數
        BufferedReader br = null;
        
        //------------------------------------------      
        try{   
            // 建立檔案讀取物件  
            br = new BufferedReader(new FileReader(new File("exams.csv")));            
            
            // 逐行讀入檔案內容
            //---------------------            
            String line;        
            while ((line = br.readLine()) != null) {  
                // 顯示讀入的資料           
                System.out.println(line);
                
                // 切割欄位內容
                String items[] = line.split(",");
                
                String stuNo = items[0].trim();
                String stuName = items[1].trim();
                String gender = items[2].trim();
                int chi = Integer.parseInt(items[3].trim());
                
                // 顯示切割欄位內容
                System.out.println(stuNo);
                System.out.println(stuName);
                System.out.println(gender);
                System.out.println(chi);
                System.out.println("-------------------------");               
            }                   
            //---------------------            
        }catch(IOException e){
            System.out.println("發生錯誤, 原因: " + e);                     
            return;
        }finally{
            // 關閉reader
            if(br != null){
                br.close();              
            }    
        }  
        //------------------------------------------         
    }    
}
```


<br/>

## (2) 讀入一個csv檔, 寫出一個csv檔

```
Java專案
   |__ Main.java
   |__ exams.csv (輸入檔)
   |__ out.csv (輸出檔, 程式產生)   
```

### Main.java
```java
import java.io.*;

class Main {
    public static void main(String[] args) throws IOException {
        // 宣告檔案讀取及寫出變數
        BufferedReader br = null;
        BufferedWriter bw = null;
        
        //------------------------------------------      
        try{   
            // 建立檔案讀取及寫出物件  
            br = new BufferedReader(new FileReader(new File("exams.csv"))); 
            bw = new BufferedWriter(new FileWriter(new File("out.csv")));
            
            // 逐行讀入檔案內容
            //--------------------- 
            boolean firstLine = true;            
            String line;     
            
            while ((line = br.readLine()) != null) { 
                // 顯示讀入的資料              
                System.out.println(line);
                
                // 切割欄位內容
                String items[] = line.split(",");
                
                String stuNo = items[0].trim();
                String stuName = items[1].trim();
                String gender = items[2].trim();
                int chi = Integer.parseInt(items[3].trim());  
                
                // 將內容寫出檔案
                String data = stuNo + "," + stuName + "," + gender + "," + chi;
                
                if(firstLine){
                    bw.write(data);
                    firstLine=false;
                }else{
                    bw.write(("\n"));
                    bw.write(data);                
                }                
            }                   
            //---------------------            
        }catch(IOException e){
            System.out.println("發生錯誤, 原因: " + e);                     
            return;
        }finally{
            // 關閉reader
            if(br != null){
                br.close();              
            }  
            
            // 關閉writer
            if(bw != null){
                bw.close();              
            }              
        }  
        //------------------------------------------         
    }    
}
```
