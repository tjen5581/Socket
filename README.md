import java.util.*;
import java.io.*; // changed these lines
import java.net.*;

public class client {
    public static void main(String[] args) throws Exception {
        Socket t = new Socket("localhost", 9999);
        System.out.println("connected");
        DataOutputStream dout = new DataOutputStream(t.getOutputStream()); // fixed typos
        BufferedReader fromServer = new BufferedReader(new InputStreamReader(t.getInputStream())); // input stream
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        while (true) {
            String tee = br.readLine();
            dout.writeUTF(tee+'\n');
            if (tee.equalsIgnoreCase("exit"))
                break;
            tee = fromServer.readLine();
            System.out.println("client: " + tee);
        }
        t.close();
    }
}
