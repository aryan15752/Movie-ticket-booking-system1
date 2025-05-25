# Movie-ticket-booking-system1
A Python-based movie ticket booking system that allows users to view movies, select showtimes, choose seats, and book tickets with ease.
import pickle

def openp():
    print("====================")
    print("\n\t\t\t\t")
    print("\t\t\t\t SCENEMA")
    print("====================")
    print("\n\t\t\t\tOPTIONS")
    print("\t\t\t\t1.LOGIN")
    print("\t\t\t\t2.SIGN UP")
    n=int(input("ENTER YOUR CHOICE(1/2):"))
    if n==1:
        login()
    elif n==2:
        signup()
    else:
        print("PLEASE CHOOSE FROM ABOVE OPTION!!")
        openp()

def signup():
    f=open("info.dat","ab")
    n=input("ENTER USERNAME OF YOUR CHOICE:")
    p=input("ENTER PASSWORD OF YOUR CHOICE:")
    data=[n,p]
    pickle.dump(data,f)
    f.close()
    print("RECORD ADDED SUCCESSFULLY!!\n\n")
    welcome()

def login():
    f=open("info.dat","rb")
    print("\n\t\t\tLOGIN!")
    un=input("ENTER YOUR USERNAME:")
    flag=0
    flag1=0
    while True:
        try:
            s=pickle.load(f)
            if s[0]==un:
                pin=input("ENTER YOUR PASSWORD:")
                flag=1
                if s[1]==pin:
                    print("LOGIN SUCCESSFULL!!\n\n")
                    flag1=1
                    welcome()
        except EOFError:
            break
    if flag==0:
        print("INCORRECT USERNAME!")
        flag1=2
        login()
    if flag1==0:
        print("INCORRECT PASSWORD!")
        login()

def welcome():
    ans="y"
    while ans in "Yy":
        print("====================================")
        print("[][][][][][][][][][][][][][][][][][]")
        print("[]\t\t\t\t\t\t\t\t\t[]")
        print("[]\t\t\t\t SCENEMA\t\t\t\t[]")
        print("[]\t\t\t\t\t\t\t\t\t[]")
        print("[][][][][][][][][][][][][][][][][][]")
        print("------------------------------------")
        print("\t\t\t\t||WELCOME||\t\t\t\t")
        print("------------------------------------")
        print("\tOPTIONS")
        print("1.HOME")
        print("2.FILTER")
        print("3.THEATRE")
        print("4.MY BOOKINGS")
        print("5.EXIT")
        n=int(input("ENTER YOUR CHOICE(1/2/3/4/5):"))
        if n==1:
            home()
        elif n==2:
            movies()
        elif n==3:
            city()
        elif n==4:
            prebooks()
        elif n==5:
            print("\t\t\t\t*******")
            break
        else:
            print("PLEASE SELECT FROM ABOVE!!")
            welcome()
        ans=input("DO U WANT TO CONTINUE(y/n):")

def home():
    print("=====================================")
    print("[][][][][][][][][][][][][][][][][][] []")
    print("[]\t\t\t\t\t\t\t\t\t[]")
    print("[]\t\t\t\t SCENEMA\t\t\t\t[]")
    print("[]\t\t\t\t\t\t\t\t\t[]")
    print("[][][][][][][][][][][][][][][][][][]             ")
    print("-------------------------------------")
    print("\t\t\t\t||Home||\t\t\t\t")
    print("-------------------------------------\n")
    print("COMING SOON")
    print("****************************************")
    print("* * * * * *")
    print("* *** * *** * *** * *** * *** *")
    print("* * ** * ** * ** * ** * **")
    print("* * * * * * * * * * *")
    print("* *** * *** * *** * *** * *** *")
    print("* * ** * ** * ** * ** * **")
    print("* * * * * * * * * * *")
    print("* * * * * *")
    print("****************************************")
    print("PUSHPA:THE RISE 83   SPIDER-MAN:NO   SHOOTER ")
    print("PART 01              WAY HOME       \n")
    print("RECOMMENDED")
    print("****************************************")
    print("* * * * * *")
    print("* * * * * *")
    print("* * * * * *")
    print("* 0002 * 0200 * 0300 * 0040 *")
    print("* * * * * *")
    print("* * * * * *")
    print("* * * * * *")
    print("* * * * * *")
    print("****************************************")
    print("PARASITE           VENOM           URI           1920\n")
    print("OPTIONS")
    print("1.SELECT FROM ABOVE")
    print("2.EXIT")
    m=int(input("ENTER YOUR CHOICE(1/2):"))
    if m==1:
        n=input("ENTER THE MOVIE ID GIVEN INSIDE THE POSTER:")
        last(n)
    elif m==2:
        welcome()
    else:
        print("PLEASE SELECT FROM ABOVE!!")
        home()

def movies():
    print("1.DRAMA")
    print("2.ACTION")
    print("3.HORROR")
    print("4.COMEDY")
    print("5.SCI FI")
    n=int(input("ENTER YOUR CHOICE(1/2/3/4/5):"))
    if n==1:
        sortting(1)
    elif n==2:
        sortting(2)
    elif n==3:
        sortting(3)
    elif n==4:
        sortting(4)
    elif n==5:
        sortting(5)
    else:
        print("PLEASE SELECT FROM ABOVE!!")
        movies()

def sortting(a):
    p=a
    s=1
    if p==1:
        s="DRAMA"
    elif p==2:
        s='ACTION'
    elif p==3:
        s='HORROR'
    elif p==4:
        s='COMEDY'
    elif p==5:
        s='SCI FI'
    dr=[]
    f=open("movies.dat","rb")
    while True:
        try:
            r=pickle.load(f)
            if r[4]==s:
                dr.append(r)
        except EOFError:
            break
    if dr!=[]:
        lang(dr)
    else:
        print("NO MOVIES AVAILABLE,PLEASE SELECT ANOTHER GENRE!!")
        movies()
    f.close()

def lang(a):
    d=a
    print("1.HINDI")
    print("2.ENGLISH")
    sh=[]
    n=int(input("SELECT LANGUAGE(1/2):"))
    if n==1:
        for i in d:
            if i[2]=="HINDI":
                sh.append(i)
    elif n==2:
        for i in a:
            if i[2]=="ENGLISH":
                sh.append(i)
    else:
        print("PLEASE SELECT FROM ABOVE!!")
    display(sh)

def display(a):
    print("%10s"%"MOVIE_ID","%14s"%"NAME","%15s"%"LANGUAGE","%14s"%"THEATRE","%15s"%"GENRE","%11s"%"DATE","%15s"%"TIME")
    print("---------------------------------------------------------------------------------------------")
    for i in a:
        print("%7s"%i[0],"%16s"%i[1],"%15s"%i[2],"%16s"%i[3],"%15s"%i[4],"%14s"%i[5],"%11s"%i[6])
    n=input("ENTER THE MOVIE ID OF THE MOVIE YOU WANT TO WATCH:")
    last(n)

def last(a):
    f=open("movies.dat","rb")
    L=[]
    flag=0
    A=a
    while True:
        try:
            p=pickle.load(f)
            if p[0]==str(A):
                L=L+p
                flag=1
        except EOFError:
            break
    if flag==0:
        print("INVAILID MOVIE ID!!!")
        movies()
    n=input("SELECT SEAT NO.(1-30):")
    print("1.POPCORN")
    print("2.COLD DRINK")
    print("3.FRIES")
    print("4.BURGER")
    print("5.NONE")
    v=int(input("\nSELECT SNACKS FROM ABOVE OPTION(1/2/3/4/5):"))
    if v not in [1,2,3,4,5]:
        print("\t\t\tPLEASE SELECT FROM ABOVE!!")
        last(A)
    ticket(L,n,v)

def ticket(a,b,c):
    l=a
    print("%10s"%"MOVIE_ID","%14s"%"NAME","%15s"%"LANGUAGE","%14s"%"THEATRE","%15s"%"GENRE","%11s"%"DATE","%15s"%"TIME")
    print("---------------------------------------------------------------------------------------------")
    print("%7s"%l[0],"%16s"%l[1],"%15s"%l[2],"%16s"%l[3],"%15s"%l[4],"%14s"%l[5],"%11s"%l[6])
    if c==1:
        s="POPCORN"
    if c==2:
        s="COLD DRINK"
    if c==3:
        s="FRIES"
    if c==4:
        s="BURGER"
    if c==5:
        s="NONE"
    print("\n\n\t SEATNO:",b)
    print("\t SNACKS:",s)
    n=input("\nDO YOU WANT TO CONFIRM YOUR BOOKING(y/n):")
    if n in "Yy":
        z=input("ENTER UR USERNAME:")
        print("\n\t\t\tBOOKING SUCCESSFULL!!")
        o=[a,b,s,z]
        store(o)
    else:
        ans=input("DO YOU TO CONTINUE SEARCHING FOR MOVIES(y/n):")
        if ans in "yY":
            welcome()
        else:
            print("\t\t\t*********")

def city():
    print("\nSELECT CITY FROM BELOW")
    print("1.MUMBAI")
    print("2.DELHI")
    print("3.HYDERABAD")
    print("4.CHENNAI")
    n=int(input("ENTER YOUR CHOICE(1/2/3/4):"))
    if n not in [1,2,3,4]:
        print("\nPLEASE SELECT FROM ABOVE OPTIONS!!\n\n")
        city()
    theatre(n)

def theatre(a):
    if a==1:
        mumbai()
    elif a==2:
        delhi()
    elif a==3:
        hyderabad()
    elif a==4:
        chennai()

def mumbai():
    print("\n1.THEATRE A")
    print("2.THEATRE B")
    n=input("ENTER YOUR CHOICE:")
    sh=[]
    f=open("movies.dat","rb")
    if n=="1":
        while True:
            try:
                s=pickle.load(f)
                if s[3]=="THEATRE A":
                    sh.append(s)
            except EOFError:
                break
    elif n=="2":
        while True:
            try:
                s=pickle.load(f)
                if s[3]=="THEATRE B":
                    sh.append(s)
            except EOFError:
                break
    else:
        print("PLEASE SELECT FROM ABOVE!!")
    mumbai()
    display(sh)

def delhi():
    print("\n1.THEATRE C")
    print("2.THEATRE D")
    n=input("ENTER YOUR CHOICE:")
    sh=[]
    f=open("movies.dat","rb")
    if n=="1":
        while True:
            try:
                s=pickle.load(f)
                if s[3]=="THEATRE C":
                    sh.append(s)
            except EOFError:
                break
    elif n=="2":
        while True:
            try:
                s=pickle.load(f)
                if s[3]=="THEATRE D":
                    sh.append(s)
            except EOFError:
                break
    else:
        print("PLEASE SELECT FROM ABOVE!!")
    delhi()
    display(sh)

def hyderabad():
    print("\n1.THEATRE E")
    print("2.THEATRE F")
    n=input("ENTER YOUR CHOICE:")
    sh=[]
    f=open("movies.dat","rb")
    if n=="1":
        while True:
            try:
                s=pickle.load(f)
                if s[3]=="THEATRE E":
                    sh.append(s)
            except EOFError:
                break
    elif n=="2":
        while True:
            try:
                s=pickle.load(f)
                if s[3]=="THEATRE F":
                    sh.append(s)
            except EOFError:
                break
    else:
        print("PLEASE SELECT FROM ABOVE!!")
    hyderabad()
    display(sh)

def chennai():
    print("\n1.THEATRE G")
    print("2.THEATRE H")
    n=input("ENTER YOUR CHOICE:")
    sh=[]
    f=open("movies.dat","rb")
    if n=="1":
        while True:
            try:
                s=pickle.load(f)
                if s[3]=="THEATRE G":
                    sh.append(s)
            except EOFError:
                break
    elif n=="2":
        while True:
            try:
                s=pickle.load(f)
                if s[3]=="THEATRE H":
                    sh.append(s)
            except EOFError:
                break
    else:
        print("PLEASE SELECT FROM ABOVE!!")
    chennai()
    display(sh)

def store(a):
    f=open("BOOKINGS.dat","ab")
    pickle.dump(a,f)
    f.close()

def prebooks():
    f=open("BOOKINGS.dat","rb")
    n=input("ENTER YOUR USERNAME:")
    flag=0
    while True:
        try:
            s=pickle.load(f)
            if s[-1]==n:
                l=s[0]
                print("\t\t\t\t\t\t ")
                print("\t\t\t\t\t\t ]]BOOKINGS[[")
                print("\n%10s"%"MOVIE_ID","%14s"%"NAME","%15s"%"LANGUAGE","%14s"%"THEATRE","%15s"%"GENRE","%11s"%"DATE","%15s"%"TIME")
                print("---------------------------------------------------------------------------------------------")
                print("%7s"%l[0],"%16s"%l[1],"%15s"%l[2],"%16s"%l[3],"%15s"%l[4],"%14s"%l[5],"%11s"%l[6])
                print("\n\n\t SEATNO:",s[1])
                print("\t SNACKS:",s[2])
                flag=1
        except EOFError:
            break
    if flag==0:
        print("NO BOOKINGS!!!")

def ADDdata():
    f=open("movies.dat","ab")
    ans="y"
    print("KINDLY FILL ALL THE RECORD IN CAPITAL LETTERS ONLY!!\n")
    while ans in "Yy":
        s=input("ENTER MOVIE ID:")
        n=input("ENTER THE NAME OF THE MOVIE:")
        la=input("ENTER LANGUAGE(ENGILHS/HINDI):")
        nT=input("ENTER THE NAME OF THE THEATRE:")
        g=input("ENTER THE GENRE:")
        d=input("ENTER THE DATE OF THE MOVIE(DD-MM-YYYY):")
        t=input("TIMINNGS(SPECIFY AM/PM):")
        data=[s,n,la,nT,g,d,t]
        pickle.dump(data,f)
        ans=input("DO YOU WANT TO ADD MORE RECORDS(Y/N):")
    f.close()

def DISPdata():
    s=[]
    f=open("movies.dat","rb")
    print("%10s"%"MOVIE_ID","%14s"%"NAME","%15s"%"LANGUAGE","%14s"%"THEATRE","%15s"%"GENRE","%11s"%"DATE","%15s"%"TIME")
    print("---------------------------------------------------------------------------------------------")
    while True:
        try:
            i=pickle.load(f)
            print("%7s"%i[0],"%16s"%i[1],"%15s"%i[2],"%16s"%i[3],"%15s"%i[4],"%14s"%i[5],"%11s"%i[6])
        except EOFError:
            break
    f.close()

def MODIFYdata():
    f=open("movies.dat","rb")
    L2=[]
    found=False
    n=input("ENTER THE MOVIES ID TO MODIFY DATE AND TIME:")
    while True:
        try:
            s=pickle.load(f)
            if s[0]==n:
                m=input("ENTER THE UPDATED DATE(DD-MM-YYYY):")
                s[5]=m
                P=input("ENTER THE UPDATED TIME(SPECIFY AM/PM):")
                s[6]=P
                print("RECORD UPDATED!!")
                found=True
                L2.append(s)
            else:
                L2.append(s)
        except EOFError:
            break
    with open("movies.dat","wb") as f:
        for n in L2:
            pickle.dump(n,f)
    f.close()

def DELdata():
    f=open("movies.dat","rb")
    l=[]
    found=False
    n=input("ENTER THE MOVIE ID TO BE DELETED:")
    while True:
        try:
            s=pickle.load(f)
            if s[0]==n:
                found=True
            else:
                l.append(s)
        except EOFError:
            break
    if found==False:
        print("MOVIE NOT FOUND!")
    else:
        print("MOVIE DELETED!")
    with open("movies.dat","wb") as f:
        for n in l:
            pickle.dump(n,f)
    f.close()

def SEARCH():
    s=[]
    f=open("movies.dat","rb")
    Found=False
    r=input("ENTER THE MOVIE ID TO SEACRCH:")
    while True:
        try:
            s=pickle.load(f)
            if s[0]==r:
                print(s)
                Found=True
                break
        except EOFError:
            break
    if Found==False:
        print("MOVIE NOT FOUND")
    f.close()

def readuser():
    f=open("info.dat","rb")
    while True:
        try:
            s=pickle.load(f)
            print(s)
        except EOFError:
            break
    f.close()

def MENU():
    print(" ")
    print("\t\t\t ===SCENEMA===")
    print("\t\t\t ")
    print("\t\t\t STAFF MENU")
    print("\n\t ")
    print("\t OPTIONS:")
    print("1.DISPLAY")
    print("2.ADD MOVIES")
    print("3.MODIFY DATE AND TIME")
    print("4.DELETE A MOVIE")
    print("5.SEARCH A MOVIE")
    print("6.VIEW USER AND PASSWORD")
    print("7.EXIT")
    print(" ")
    a=int(input("ENTER THE OPTION NUMBER:"))
    while True:
        if a==1:
            DISPdata()
        elif a==2:
            ADDdata()
        elif a==3:
            MODIFYdata()
        elif a==4:
            DELdata()
        elif a==5:
            SEARCH()
        elif a==6:
            readuser()
        elif a==7:
            print("\t\t\t\t*************")
            break
        else:
            print("**PLEASE CHOOSE FROM THE ABOVE OPTIONS**")
        b=input("\nCONTINUE THE MENU PROCESS(Y/N)?:")
        if b=="Y" or b=="y":
            MENU()
        else:
            print("\n\t\t\t\t*************")
            break
        break

def Staffsignup():
    f=open("staffinfo.dat","ab")
    n=input("ENTER USERNAME OF YOUR CHOICE:")
    p=input("ENTER PASSWORD OF YOUR CHOICE:")
    data=[n,p]
    pickle.dump(data,f)
    f.close()
    print("RECORD ADDED SUCCESSFULLY!!\n\n")
    MENU()

def Stafflogin():
    f=open("staffinfo.dat","rb")
    print("\n\t\t\tLOGIN!")
    un=input("ENTER YOUR USERNAME:")
    flag=0
    flag1=0
    while True:
        try:
            s=pickle.load(f)
            if s[0]==un:
                pin=input("ENTER YOUR PASSWORD:")
                flag=1
                if s[1]==pin:
                    print("LOGIN SUCCESSFULL!!\n\n")
                    flag1=1
                    MENU()
        except EOFError:
            break
    if flag==0:
        print("INCORRECT USERNAME!")
        flag1=2
        Stafflogin()
    if flag1==0:
        print("INCORRECT PASSWORD!")
        Stafflogin()

def startS():
    print("\t\t\t\t************")
    print("\t\t\t\t SCENEMA")
    print("\n\n1.STAFF LOGIN")
    print("2.STAFF SIGNUP")
    n=int(input("ENTER YOUR CHOICE(1/2):"))
    if n==1:
        Stafflogin()
    elif n==2:
        Staffsignup()
    else:
        print("PLEASE CHOOSE FROM ABOVE OPTION!!")
        openp()

print("\t\t\t\t************")
print("\t\t\t\t SCENEMA")
print("\n\n1.STAFF SCREEN")
print("2.USER SCREEN")
n=int(input("ENTER YOUR CHOICE:"))
if n==1:
    startS()
elif n==2:
    openp()
else:
    print("\nPRINT\nPLEASE SELECT FROM ABOVE OPTION")
