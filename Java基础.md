# Java基础

## io

字节流以Stream结尾，按字节方式读取，适合读取音视图

字符流按照字符方式读取，一次读取2个字节，适合读取纯文本

### 16种流

FileInputStream

FileOutputStream

FileReader

FileWriter



BufferedReader

BufferedWriter

BufferedInuputStream

BufferedOutputStream



DataInputStream

DataOutputStream



转换流（字节流转换为字符流）

ObjectInputStream

ObjectOutputStream



PrinterWriter

PrinterStream	//标准的输出流

###### 

四大家族

InputStream OutputStream Reader Writer

### FileInputStream

~~~java
//创建一个输入流
//列出子文件
File f3 = new File("D:/");
File[] fs = f3.listFiles();
//遍历
~~~



