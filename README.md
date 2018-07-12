# Java

----
## 1.Thừa kế
> Cú pháp thừa kế

    class ten_lop_con extends ten_lop_cha
    {
    //cac phuong thuc va cac truong
    }
Từ khóa extends chỉ rằng bạn đang tạo một lớp mới mà kế thừa từ một lớp đang tồn tại. Trong Java, một lớp mà được kế thừa được gọi là một lớp cha. Lớp mới được gọi là lớp con.
Trong ví dụ sau, Programmer là lớp con và Employee là lớp cha. Mối quan hệ giữa hai lớp là Programmer IS-A Employee. Nghĩa là Programmer là một kiểu của Employee.


    class Employee
    {  
     float salary=40000;  
    }  
    class Programmer extends Employee
    {  
     int bonus=10000;  
      public static void main(String args[])
      {  
       Programmer p=new Programmer();  
       System.out.println("Luong Lap trinh vien la:"+p.salary);  
       System.out.println("Bonus cua Lap trinh vien la:"+p.bonus);  
      }  
    }  

> Ở trên, đối tượng Programmer có thể truy cập trường của riêng lớp nó cũng như của lớp Employee, đó là ví dụ cho tính tái sử dụng.


#2.ĐA HÌNH
Tính đa hình trong Java là một khái niệm mà từ đó chúng ta có thể thực hiện một hành động đơn theo nhiều cách khác nhau. Tính đa hình được suy ra từ hai từ Hy Lạp là Poly và Morphs. Poly nghĩa là nhiều và morphs nghĩa là hình, dạng. Có hai kiểu đa hình trong Java: Đa hình tại compile time và đa hình runtime. Chúng ta có thể thực hiện tính đa hình trong Java bởi nạp chồng phương thức và ghi đè phương thức.
Nếu bạn nạp chồng phương thức static trong Java, thì đó là ví dụ về đa hình tại compile time. Ở chương này chúng sẽ tập trung vào đa hình tại runtime trong Java.
Điều quan trọng để biết là có cách nào truy cập một đối tượng qua các biến tham chiếu. Một biến tham chiếu có thể chỉ là một kiểu. Khi được khai báo, kiểu của biến tham chiếu này không thể thay đổi.
Biến tham chiếu có thể được gán cho những đối tượng khác được cung cấp mà không được khai báo final. Kiểu của biến tham chiếu sẽ xác định phương thức mà có thể được triệu hồi trên đối tượng.
Một biến tham chiếu có thể được hướng đến bất kì đối tượng với kiểu khai báo hoặc bất kì kiểu con nào của kiểu khai báo. Một biến tham chiếu có thể được khai báo như là một class hoặc một interface.

1. Đa hình tại runtime trong Java

Đa hình tại runtime là một tiến trình mà trong đó một lời gọi tới một phương thức được ghi đè được xử lý tại runtime thay vì tại compile time. Trong tiến trình này, một phương thức được ghi đè được gọi thông qua biến tham chiếu của một lớp cha. Việc quyết định phương thức được gọi là dựa trên đối tượng nào đang được tham chiếu bởi biến tham chiếu.
Trước khi tìm hiểu về đa hình tại runtime, chúng ta cùng tìm hiểu về Upcasting.


2.Upcasting là gì?

Khi biến tham chiếu của lớp cha tham chiếu tới đối tượng của lớp con, thì đó là Upcasting. Ví dụ:

    class A{}  
    class B extends A{}  
    A a=new B();//day la upcasting

Ví dụ về đa hình tại runtime trong Java
Trong ví dụ, chúng ta tạo hai lớp Bike và Splendar. Lớp Splendar kế thừa lớp Bike và ghi đè phương thức run() của nó. Chúng ta gọi phương thức run bởi biến tham chiếu của lớp cha. Khi nó tham chiếu tới đối tượng của lớp con và phương thức lớp con ghi đè phương thức của lớp cha, phương thức lớp con được triệu hồi tại runtime.

Khi việc gọi phương thức được quyết định bởi JVM chứ không phải Compiler, vì thế đó là đa hình tại runtime.

    class Bike{  
      void run(){System.out.println("dang chay");}  
    }  
    class Splender extends Bike{  
      void run(){System.out.println("chay an toan voi 60km");}  
  
      public static void main(String args[]){  
        Bike b = new Splender();//day la upcasting  
        b.run();  
      }  
    }  

Ví dụ thực về đa hình tại runtime trong Java
Giả sử Bank là một lớp cung cấp phương thức để lấy lãi suất. Nhưng lãi suất lại khác nhau giữa từng ngân hàng. Ví dụ, các ngân hàng VCB, AGR và CTG có thể cung cấp các lãi suất lần lượt là 8%, 7% và 9%. (Ví dụ này cũng có trong chương ghi đè phương thức nhưng không có Upcasting)

    class Bank{  
    int getRateOfInterest(){return 0;}  
    }  
  
    class VCB extends Bank{  
    int getRateOfInterest(){return 8;}  
    }  
  
    class AGR extends Bank{  
    int getRateOfInterest(){return 7;}  
    }  
    class CTG extends Bank{  
    int getRateOfInterest(){return 9;}  
    }  
  
    class Test3{  
    public static void main(String args[]){  
    Bank b1=new VCB();  
    Bank b2=new AGR();  
    Bank b3=new CTG();  
    System.out.println("VCB lai suat la: "+b1.getRateOfInterest());  
    System.out.println("AGR lai suat la: "+b2.getRateOfInterest());  
    System.out.println("CTG lai suat la: "+b3.getRateOfInterest());  
    }  
    } 
    )
3.Đa hình tại runtime trong Java với thành viên dữ liệu

Phương thức bị ghi đè không là thành viên dữ liệu, vì thế đa hình tại runtime không thể có được bởi thành viên dữ liệu. Trong ví dụ sau đây, cả hai lớp có một thành viên dữ liệu là speedlimit, chúng ta truy cập thành viên dữ liệu bởi biến tham chiếu của lớp cha mà tham chiếu tới đối tượng lớp con. Khi chúng ta truy cập thành viên dữ liệu mà không bị ghi đè, thì nó sẽ luôn luôn truy cập thành viên dữ liệu của lớp cha.

Qui tắc: Đa hình tại runtime không thể có được bởi thành viên dữ liệu.

    class Bike{  
     int speedlimit=90;  
    }  
    class Honda3 extends Bike{  
     int speedlimit=150;  
  
     public static void main(String args[]){  
      Bike obj=new Honda3();  
      System.out.println(obj.speedlimit);//90  
    }
 
4.Đa hình tại runtime trong Java với kế thừa nhiều tầng (Multilevel)

Bạn theo dõi ví dụ sau:

    class Animal{  
    void eat(){System.out.println("an");}  
    }  
  
    class Dog extends Animal{  
    void eat(){System.out.println("an hoa qua");}  
    }  
  
    class BabyDog extends Dog{  
    void eat(){System.out.println("uong sua");}  
  
    public static void main(String args[]){  
    Animal a1,a2,a3;  
    a1=new Animal();  
    a2=new Dog();  
    a3=new BabyDog();  
  
    a1.eat();  
    a2.eat();  
    a3.eat();  
    }  
    }
Và:

    class Animal{  
    void eat(){System.out.println("animao dang an...");}  
    }  
  
    class Dog extends Animal{  
    void eat(){System.out.println("dog dang an...");}  
    }  
  
    class BabyDog1 extends Dog{  
    public static void main(String args[]){  
    Animal a=new BabyDog1();  
    a.eat();  
    }} 

Vì, BabyDog không ghi đè phương thức eat(), do đó phương thức eat() của lớp Dog() được triệu hồi.

#3.QUAN HÊ KÊT HỌP HAS_A

Nếu một lớp có một tham chiếu thực thể, thì nó được biết đến như là một lớp có quan hệ HAS-A. Giả sử một tình huống, đối tượng Employee chứa nhiều thông tin như id, name, eamailID, … Nó gồm một hoặc nhiều đối tượng address mà có thông tin riêng như city, state, country, zipcode, … như sau:

    class Employee{  
    int id;  
    String name;  
    Address address; //Address la mot lop 
    ...  
    } 

Trong tình huống như vậy, Emloyee có một address là tham chiếu thực thể, vì thế mối quan hệ là Employee HAS-A address.

Tại sao và khi nào sử dụng quan hệ HAS-A
Sử dụng quan hệ HAS-A giúp làm tăng tính tái sử dụng của code. Và khi không có mối quan hệ IS-A, thì quan hệ HAS-A là lựa chọn tốt nhất.

Tính kế thừa nên chỉ được sử dụng nếu mối quan hệ IS-A được duy trì thông qua suốt vòng đời của đối tượng có liên quan; nếu không thì, quan hệ HAS-A là lựa chọn tốt nhất.

Ví dụ đơn giản về quan hệ HAS-A trong Java
Trong ví dụ, chúng ta tạo tham chiếu của lớp Operation trong lớp Circle.

    class Operation{  
     int square(int n){  
      return n*n;  
     }  
    } 
  
    class Circle{  
     Operation op; //quan hệ HAS-A  
     double pi=3.14;  
    
     double area(int radius){  
       op=new Operation();  
       int rsquare=op.square(radius); //tai su dung code (vi du: uy quyen cho loi goi phuong thuc).  
       return pi*rsquare;  
     }  
  
     
    
     public static void main(String args[]){  
       Circle c=new Circle();  
       double result=c.area(5);  
       System.out.println(result);  
     }  
    }

Ví dụ
Như trong ví dụ trên đã đề cập, Employee có một đối tượng là Address, đối tượng này chứa thông tin riêng như city, state, country, … Trong tình huống này, mối quan hệ là Employee HAS-A address.

Tệp Address.java có nội dung:

     public class Address {  
        String city,state,country;  
  
        public Address(String city, String state, String country) {  
            this.city = city;  
          this.state = state;  
            this.country = country;  
        }  
  
        }   
   
Tệp Emp.java có nội dung sau:

     public class Emp {  
     int id;  
     String name;  
     Address address;  
  
     public Emp(int id, String name,Address address) {  
      this.id = id;  
       this.name = name;  
       this.address=address;  
     }  
  
     void display(){  
     System.out.println(id+" "+name);  
     System.out.println(address.city+" "+address.state+" "+address.country);  
     }  
  
     public static void main(String[] args) {  
     Address address1= new Address("hanoi","HN","vietnam");  
     Address address2=new Address("hadong","HN","vietnam");  
  
     Emp e=new Emp(111,"hoang",address1);  
     Emp e2=new Emp(112,"thanh",address2);  
      
     e.display();  
     e2.display();  
      
     }  
     }  

Chạy chương trình trên sẽ cho kết quả:

     Output:
     111 hoang
     hanoi HN vietnam
     112 thanh
     hadong HN vietnam    


