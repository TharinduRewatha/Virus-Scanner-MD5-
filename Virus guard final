//N.M.Tharindu rewatha
#include <iostream>
#include <windows.h> 
#include <fstream>
#include <string>
#include <unordered_set>
#include <sstream>
#include <conio.h>		//_getch()

#define BUFSIZE 1024
#define MD5LEN  16
void MaximizeOutputWindow();	//Maximize the CLI window when the code starts

using namespace std;


DWORD main()
{
    MaximizeOutputWindow();
    DWORD cryptStatus = 0;
    BOOL hashResult = FALSE;
    BYTE fileSizeToHash[BUFSIZE];
    HCRYPTPROV cryptProv = 0;
    HCRYPTHASH hash = 0;
    HANDLE file = 0;
    DWORD hashNumbCount = 0;
    DWORD hashRead = 0;
    BYTE getHashValue[MD5LEN];

    CHAR numberConvert[] = "0123456789abcdef"; //hex decimal conversion

    LPCWSTR DirectoryOfTheFile = L"C:\\Users\\nmrth\\Downloads\\WhatsApp Image 2020-07-22 at 3.08.34 PM.jpeg"; //Name of the file that user is scanning


    // Logic to check usage goes here.
    file = CreateFile(DirectoryOfTheFile, GENERIC_READ, FILE_SHARE_READ, NULL, OPEN_EXISTING, FILE_FLAG_SEQUENTIAL_SCAN, NULL);

    // Get handle to the crypto provider
    if (!CryptAcquireContext( &cryptProv, NULL, NULL, PROV_RSA_FULL, CRYPT_VERIFYCONTEXT))

    {
       cryptStatus = GetLastError();
       cout << "CryptAcquireContext failed: %d\n" << cryptStatus;
       CloseHandle(file);
       return cryptStatus;
    }

    if (!CryptCreateHash(cryptProv, CALG_MD5, 0, 0, &hash))

    {
       cryptStatus = GetLastError();
       cout << "CryptAcquireContext failed: %d\n" << cryptStatus;
       CloseHandle(file);
       CryptReleaseContext(cryptProv, 0);
       return cryptStatus;
    }

    while (hashResult = ReadFile(file, fileSizeToHash, BUFSIZE, &hashRead, NULL))

    {
        if (0 == hashRead)
        {
           break;
        }


        if (!CryptHashData(hash, fileSizeToHash, hashRead, 0))

        {
             cryptStatus = GetLastError();
             cout <<"CryptHashData failed: %d\n" << cryptStatus;
             CryptReleaseContext(cryptProv, 0);
             CryptDestroyHash(hash);
             CloseHandle(file);
             return cryptStatus;
        }
    }

    if (!hashResult)

    {
       cryptStatus = GetLastError();
       cout << "ReadFile failed: %d\n" <<  cryptStatus;
       CryptReleaseContext(cryptProv, 0);
       CryptDestroyHash(hash);
       CloseHandle(file);
       return cryptStatus;
    }

    hashNumbCount = MD5LEN;//Get the number of charactors in the hash as an input

    if (CryptGetHashParam(hash, HP_HASHVAL, getHashValue, &hashNumbCount, 0))

    {
       fstream checkFile("Test1.txt");//Compare the md5 hash with
       string line;
       unordered_set < string > finalHash;
       while (checkFile >> line)
        {
            finalHash.insert(line);
        }


        ostringstream showHash;

        for (int i = 0; i < hashNumbCount; i++)
        {
                showHash << numberConvert[getHashValue[i] >> 4] <<
                numberConvert[getHashValue[i] & 0xf];//Printing hash value
        }

        string hashVal(showHash.str());//Hold the hash value

        cout << "\x1B[93m\t\t\t\t\t\t\t\t\t\t\tAloe there we are super exited to have you on board\033[0m\t\t";

        cout << "\t\t\t\t\t\t\t\t\t\t\tPress any key to continue";

        _getch();

        system("CLS");

        cout << "\n\t\t\t\t\t\t\t\t\t     ---- MD5 hash value of your file is :  " << hashVal << " -----\n\n";
        //Infected
        if (finalHash.find(hashVal) != finalHash.end())
        {

            cout << "\033[3;43;30m\t\t\t\t\t\t\t\t\t\t\t\t\t***THREAT DITECTED!!!!***\033[0m\t\t" << endl;

            cout << "\x1B[36m\t\t\t\t\t\t\t\tIt seems something is wrong.There is a clear risk of continuing without taking necessary actions!!\033[0m"<< endl;


        }
        //No threats
        else
        {
            cout <<"\033[3;43;30m\t\t\t\t\t\t\t\t\t\t\t\t\t NO THREATS DITECTED!!\033[0m\t\t"<< endl;

            cout << "\x1B[36m\t\t\t\t\t\t\t\t\t\t\tNothing is wrong with your file.You can continue!!\033[0m\t\t";
        }

        cout << "\x1B[32m\n\t\t\t\t\t\t\t\t\t\t\t\t\t\t\t     A virus scanner by Tharindu Rewatha\033[0m\t\t";

        cout << "\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n";
    }

    else
    {
        cryptStatus = GetLastError();

        cout << "CryptGetHashParam failed: %d\n" << cryptStatus;
    }
    return 0;
}
void MaximizeOutputWindow()//Maximize the window
{

    HWND consoleWindow = GetConsoleWindow();	// This gets the value Windows uses to identify  output window 
    ShowWindow(consoleWindow, SW_MAXIMIZE);	// this mimics clicking on its' maximize button
}
