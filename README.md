import java.io.BufferedInputStream;
import java.io.File;
import java.io.FileInputStream;
import java.io.OutputStream;
import java.net.InetAddress;
import java.net.ServerSocket;
import java.net.Socket;
public class FileServer
{
public static void main(String[] args) throws Exception
{
//Initialize Sockets
ServerSocket ssock = new ServerSocket(5000);
Socket socket = ssock.accept();
//The InetAddress specification
InetAddress IA = InetAddress.getByName("localhost");
//Specify the file
File file = new File("C:/GAYATHRI/Sample.txt");
FileInputStream fis = new FileInputStream(file);
BufferedInputStream bis = new BufferedInputStream(fis);
//Get socket's output stream
OutputStream os = socket.getOutputStream();
//Read File Contents into contents array
byte[] contents;
long fileLength = file.length();
long current = 0;
long start = System.nanoTime();
while(current!=fileLength){
int size = 10000;
if(fileLength - current >= size)
current += size;
else{
size = (int)(fileLength - current);
current = fileLength;
}
contents = new byte[size];
bis.read(contents, 0, size);
os.write(contents);
System.out.print("Sending file ... "+(current*100)/fileLength+"% complete!");
}
os.flush();
//File transfer done. Close the socket connection!
socket.close();ssock.close();
System.out.println("File sent succesfully!");
} }
_______&&_______&&_
import java.io.BufferedOutputStream;
import java.io.FileOutputStream;
import java.io.InputStream;
import java.net.InetAddress;
import java.net.Socket;
public class FileClient {
public static void main(String[] args) throws Exception{
//Initialize socket
Socket socket = new Socket(InetAddress.getByName("localhost"), 5000);
byte[] contents = new byte[10000];
//Initialize the FileOutputStream to the output file's full path.
FileOutputStream fos = new FileOutputStream("C:/FOLDER/Sample1.txt");
BufferedOutputStream bos = new BufferedOutputStream(fos);
InputStream is = socket.getInputStream();
//No of bytes read in one read() call
int bytesRead = 0;
while((bytesRead=is.read(contents))!=-1)
bos.write(contents, 0, bytesRead);
bos.flush();
socket.close();
System.out.println("File saved successfully!");
}
}
}
