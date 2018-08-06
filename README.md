#include <iostream>
#include <string>
#include <stdlib.h>
#include <fstream>
#include <stdio.h>
#include <conio.h>
using namespace std;
int main()
{
    //constant administrator menu;
    const string MENU = "\nChoose one of the following options:\n"
               "\t1.VIEW SALES REPORT;\n"
                      "\t2.ADD USER;\n"
                      "\t3.EDIT USERS;\n"
                      "\t4.REORDER STOCK;\n"
                      "\t5.EXIT;\n"
                      "--> ";
    //declaring and initializing administrator login variables;
    string username,password,passWord,userName,new_user,PIN,pin;
    char login_type,menu,ans;
    int defPIN;
    username="Hummy";
    password="Hummyace";
    cout<<"ACE SUPERMAKETS\nChoose your login type:\n"
               "\t1.AS AN ADMINISTRATOR;\n"
               "\t2.AS A USER;\n"
               "\t3.AS A SALES CLERK;\n";
    cin>>login_type;
     if(login_type=='1')//login as an administrator;
   {
    cout<<"Enter your Admin user_name\n";
    cin>>userName;
    cout<<"Enter your password\n";
    cin>>passWord;
      if(userName!=username&&passWord==password||userName==username&&passWord!=password)//if either user_name or password is wrong;
    {
        cout<<"Your password does not match your user_name\n";
        exit(1);
    }
    if(userName!=username&&passWord!=password)//if both password and user name are wrong;
    {
        cout<<"Sorry you are not enrolled in this system\n";
    }

      //if both password and user name are correct;
     if(login_type=='1'&&userName==username&&passWord==password)
    {
        cout<<"successful login\nWELCOME\n";
        string Item,item;
        int Item_no,Quantity;
        double Price;
        ifstream itemlist("Items.txt");
        if (!itemlist)
        {
            cout<<"\n\n!!!!!ERROR FINDING THE ITEMS FILE!!!!!"<<endl;
            exit(1);
        }
        while(itemlist>>Item>>Item_no>>Price>>Quantity)
        {
            if(Quantity<25)
            {
                cout<<"NOTE: THE STOCK OF "<<Item<<" IS RUNNING LOW PLEASE REORDER\n";
            }
        }
        cout<<MENU<<endl;
        cin>>menu;
        if(menu=='1')//view sales report
        {
            cout<<"-----SALES REPORT-----\n";
            string U_Name,Item;
            double Price,Quantity,Payment;
            ifstream salesrep("salesreport.txt");//read from sales report file;
            while(salesrep>>U_Name>>Item>>Price>>Quantity>>Payment)
            {
                cout<<U_Name<<"\t"<<Item<<"\t"<<Price<<"\t"<<Quantity<<"\t"<<Payment<<endl;
            }
            exit(1);
        }
        if(menu=='2')//add a new user;
        {
            ifstream userin("users.txt");//read from users file;
            string USER;
            int PIN;
            cout<<"\tUSERS\n";
            while(userin>>PIN>>USER)
            {
            cout<<USER<<endl;
            }
            ofstream userout("users.txt",ios::app);//write to users file;
            do
          {
            cout<<"Enter the user_name\n";
            cin>>new_user;
            cout<<"Enter their default PIN\n";
            cin>>defPIN;
            cout<<"DO YOU WISH TO ADD ANOTHER USER?";
            cin>>ans;
            userout<<defPIN<<" "<<new_user<<endl;
          }while(ans=='y');
            cout<<"Add Successful\n";
            exit(1);
        }
    }
        if(menu=='3')//Edit existing users;
           {
            //declaring variables;
            string user,USER,pin,PIN,newpin;
            char choice,ans;
            ifstream users("users.txt");//reading from the user file;

             cout<<"Please enter the user_name of the user you want to edit\n";
             cin>>user;

             while(users>>PIN>>USER)
             {
                if(user==USER)
                {
                    cout<<"\tDETAILS\n";
                    cout<<PIN<<" "<<USER<<"\n"<<endl;
                    cout<<"Please choose from the options below:\n\n"
                     "\t1.CHANGE THE USER'S PIN;\n"//edit user menu;
                     "\t2.REMOVE THE USER;\n";
                     cin>>choice;
                     if(choice=='1')//change the user's pin;
                     {
                         if(user==USER)
                         {
                         cout<<"Please Enter The New Pin\n";
                         cin>>newpin;
                         cout<<"\n";
                         ofstream user("users2.txt",ios::app);//writing to the users2 file;
                         user<<newpin<<" "<<USER<<endl;
                         }
                        cout<<PIN<<" "<<USER<<endl;
                         exit(1);
                     }

                    else if(choice=='2')//remove or delete the user's account;
                    {
                        cout<<"Are you sure you want to remove the user?(y/n)\n";
                        cin>>ans;
                        string pin,PIN,user,USER;
                        ifstream users("users.txt");//reading from users file;
                        ofstream users2("users.txt");//writing to users2 file;
                      while(users>>PIN>>USER)
                      {
                        if(user==USER&&ans=='y')
                        {
                         cout<<PIN<<" "<<USER<<endl;
                        }
                        exit(1);
                      }
                    }
             }
            }
           }
           if(menu=='4')
           {
               char rpl;
               int Quantity,Item_no,refill;
               double Price;
               string Item;
               ifstream itemlist("Items.txt");
               while(itemlist>>Item>>Item_no>>Price>>Quantity)
               {
                   if(Quantity<25)
                   {
                       cout<<Item<<" "<<Item_no<<" "<<Price<<" "<<Quantity<<endl;
                       cout<<"Do you wish to reorder this item?(y/n)";
                       cin>>rpl;
                       if(rpl=='y')
                       {
                           refill=500-Quantity;
                           Quantity=Quantity+refill;
                           cout<<Item<<" "<<Item_no<<" "<<Price<<" "<<Quantity<<endl;
                           cout<<"reorder successful\n\n";
                       }
                       if(rpl=='n')
                          {
                              exit(1);
                          }
                   }
               }
           }
        if(menu=='5')//exit;
            {
               cout<<"Thank you for using ACE SUPERMARKETS\n";
               exit(1);
            }

   }

   if(login_type=='2')//login as a user;
   {
       string user,USER;
       int pin,PIN;
       cout<<"USERNAME: ";
       cin>>user;
       cout<<"PIN: ";
       cin>>pin;
       ifstream users("users.txt");
       while (users>>PIN>>USER)
       {
           if (user==USER&&pin==PIN)
           {
               cout<<"LOGIN SUCCESSFUL WELCOME TO ACE SUPERMARKETS "<<USER<<endl;
               string item,Item;
               int quantity,Quantity,Item_no,item_no;
               double Price,cost;
               char answer;
               ifstream itemlist("Items.txt");
               while (itemlist>>Item>>Item_no>>Price>>Quantity)
               {
                   cout<<Item<<"\t"<<Item_no<<"\t"<<Price<<"\t"<<Quantity<<endl;
               }
               cout<<"DO YOU WISH TO PURCHASE AN ITEM ?(y/n)\n";
               cin>>answer;
               if(answer=='y')
               {
                   cout<<"WHICH ITEM DO YOU WISH TO PURCHASE :";
                   cin>>item;
                   cout<<"HOW MUCH OF "<<item<<" DO YOU WISH TO PURCHASE?";
                   cin>>quantity;
                   ifstream itemlist("Items.txt");
                   while(itemlist>>Item>>Item_no>>Price>>Quantity)
                   {
                             if(item==Item&&quantity<=Quantity)
                       {
                       cost=quantity*Price;
                       Quantity=Quantity-quantity;
                       }
                        if (Item!=item||item==Item)
                       {
                        ofstream item("items2.txt",ios::app);
                        item<<Item<<" "<<Item_no<<" "<<Price<<" "<<Quantity<<endl;
                       }
                   }
                   cout<<"THE TOTAL COST FOR YOUR ITEMS IS "<<cost<<endl;
                   ofstream salesrep("salesreport.txt",ios::app);//writing to the sales report file;
                   salesrep<<user<<" "<<Item<<" "<<Price<<" "<<quantity<<" "<<cost<<endl;



               }
           }
           if (user!=USER&&pin==PIN||user==USER&&pin!=PIN)
           {
               cout<<"WRONG CREDENTIALS\n";
               exit(1);
           }
       }
   }


if (login_type=='3')//login as a sales clerk;
    {
        string UserName,UseRNamE;
        int pIn,PiN;
        cout<<"Enter your clerk's username\n";
        cin>>UserName;
        cout<<"Enter your PIN\n";
        cin>>pIn;
        ifstream clerks("clerks.txt");//reading from the clerks file;
        //confirmation of sales clerk credentials;
        while(clerks>>UseRNamE>>PiN)
        {
            if(UserName==UseRNamE&&pIn==PiN)
            {
                //declaration of variables;
                char rep;
                string U_Name,USER,item,Item;
                int quantity,Quantity,Item_no;
                double Price,payment;
                cout<<"successful login\n";
                cout<<"\tWELCOME "<<UserName<<endl;
                cout<<"Do you wish to make sales?(y/n)";
                cin>>rep;

                if(rep=='y')//if answer is yes;
                {
                    ifstream itemlist("Items.txt");//reading from items file;
                    ifstream users("users.txt");//reading from users file;
                    cout<<"Enter username\n";
                    cin>>U_Name;
                    //making sales;
                    while(users>>PIN>>USER)
                    {
                     if (U_Name==USER)
                     { cout<<"Enter the item you want to sell\n";
                       cin>>item;
                       cout<<"Enter the quantity of "<<item<<" that you wish to sell\n";
                       cin>>quantity;
                       while(itemlist>>Item>>Item_no>>Price>>Quantity)
                       {
                        if(item==Item&&quantity<=Quantity)
                        {
                            //calculating cost(payment);
                            payment=quantity*Price;
                            ofstream salesrep("salesreport.txt",ios::app);//writing to the sales report file;
                            salesrep<<U_Name<<" "<<item<<" "<<Price<<" "<<quantity<<" "<<payment<<endl;
                            cout<<"sales successful\n";
                            exit(1);
                        }
                       }
                     }
                    }
                }
            }
        }
            if(UserName!=UseRNamE&&pIn==PiN||UserName==UseRNamE&&pIn!=PiN)//if administrator user name or pin is wrong;
            {
                cout<<"Wrong clerk credentials\n";
                exit(1);
            }
            if(UserName!=UseRNamE&&pIn!=PiN)//if both the administrator pin and user name are wrong;
            {
                cout<<"Sorry you are not enrolled in the system\n";
                exit(1);
            }
            //if login type is not 1,2 or 3;
     else if(login_type!='1'||login_type!='2'||login_type!='3')
    {
        cout<<"Please choose login type that is in the options provided above\n";
        exit(1);
    }
        }

    return 0;
}
