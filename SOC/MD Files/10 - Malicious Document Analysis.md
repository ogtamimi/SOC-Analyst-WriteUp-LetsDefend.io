# Malicious Document Analysis  

# 1) Introduction to Malicious Document File Analysis  
#### [Youtube Link](https://youtu.be/Q9MhydfhzzY)

#### Macros  
*A macro is a small program written to automate repetitive tasks in Microsoft Office applications.*  

Macros are typically written in **Visual Basic for Applications (VBA)**, a programming language developed by Microsoft and supported across all Microsoft Office products.

![alt text](../Assets/lab10/1.1.png)

#### Some Tools:
1. **REMnux (Linux)**  
2. **olevba, oleid, olemeta, VMonkey** (used to extract and analyze malicious macros)  
3. **Exiftool, Strings, Xorsearch** (command-line analysis tools)

---

# 2) Static Malicious Document Analysis  
#### [Youtube Link](https://youtu.be/p3AQjmEvApI)

#### Exiftool  
Exiftool is used to display metadata information of any file.

#### Strings  
`strings` (use `-n 5` or any number to specify minimum character length) helps extract readable text from files.  

We use it to gather important information such as:
- IP addresses  
- Websites  
- Domains  
- Suspicious file locations  
- Malicious code snippets  
- Embedded malicious file names  

#### Xorsearch  
Xorsearch attempts to decrypt or uncover encoded content inside files.  

Example usage:
- `xorsearch ogt.doc http` → searches for HTTP-related strings  
- `xorsearch -p file.doc` → checks for embedded executable files inside the document  

---

## Lab  

### 1. Start the lab  
![alt text](../Assets/lab10/2.1.png)

### 2. Get the MD5 hash  
To calculate the MD5 hash, we use the Linux tool `md5sum`.  

Open the terminal in the folder containing the malicious file.

![alt text](../Assets/lab10/2.2.png)

### 3. Run md5sum  
![alt text](../Assets/lab10/2.3.png)

We obtained the hash:  
`d7e6921bfd008f707ba52dee374ff3db`

### 4. Identify the file type  
To determine the file type, we use **Exiftool**.

![alt text](../Assets/lab10/2.4.png)

The file type is: **DOC**

---

#### What is the MD5 value of the "/root/Desktop/QuestionFiles/PO-465514-180820.doc" file?  
> **ANSWER: d7e6921bfd008f707ba52dee374ff3db**

#### What is the file type of the "/root/Desktop/QuestionFiles/PO-465514-180820.doc" file?  
> **ANSWER: DOC**

---

# 3) More Details About Document File Analysis 1  
#### [Youtube Link](https://youtu.be/RRbrLuYXdTw)

#### oleid Example  
![alt text](../Assets/lab10/3.1.png)

#### olevba  
`olevba` extracts and displays all macros inside the file and highlights suspicious indicators.

![alt text](../Assets/lab10/3.2.png)

---

# 4) More Details About Document File Analysis 2  
#### [Youtube Link](https://youtu.be/ym6Crrn-D2c)

### Decoding VBA Commands

To decode VBA code inside a document:

1. Extract macros from the document:
```bash
olevba file.doc > file.vba
```

2. Deobfuscate the extracted VBA code:
```bash
olevba --deobf -reveal file.vba > file_deobf.vba
```

3. Open the `.vba` file using VSCode or any text editor for deeper analysis.

---

### VMonkey Tool  

`vmonkey` runs the malicious VBA file inside an isolated environment and simulates execution to show the results.

⚠️ NOTE:  
The `.vba` file generated from:
```bash
olevba file.doc > file.vba
```
must have all comments removed before using it with `vmonkey`.

![alt text](../Assets/lab10/4.1.png)

If we add the `--iocs` flag:
```bash
vmonkey --iocs file.vba
```
It will display Indicators of Compromise (IOCs).

---

## Lab  

```bash
Note: Before starting, install oletools:
sudo -H pip install -U oletools

Or:
pip3 install oletools
```

### 1. Check if the file contains VBA macros  

We can use either:
- `strings`
- `oleid`

![alt text](../Assets/lab10/4.2.png)

oleid results:

![alt text](../Assets/lab10/4.3.png)

Result: Yes, the file contains VBA macros.

---

### 2. Identify the macro keyword that enables malicious activity  

To do this, we need to decode the file.

### 3. Extract the VBA file  

![alt text](../Assets/lab10/4.4.png)

### 4. Open the extracted file  

Check the code (usually at the bottom section).

![alt text](../Assets/lab10/4.5.png)

We found the keyword: **Document_Open**

---

### 5. Get the author information  

Use **Exiftool**.

![alt text](../Assets/lab10/4.6.png)

---

### 6. Get the last saved time  

Use the **olemeta** tool.

![alt text](../Assets/lab10/4.7.png)

---

### 7. Identify the domain and number of IOCs  

To extract URLs and IOCs from `"Siparis_17.xls"`:

```bash
olevba Siparis_17.xls | grep http
olevba Siparis_17.xls | grep IOC
```

![alt text](../Assets/lab10/4.8.png)

Domain found:  
`hocoso.mobi`  

Number of IOCs:  
`2`

---

#### Does the file "/root/Desktop/QuestionFiles/PO-465514-180820.doc" contain a VBA macro?  
> **ANSWER: y**

#### Some malicious activity occurs when the document file "/root/Desktop/QuestionFiles/PO-465514-180820.doc" is opened. What is the macro keyword that enables this?  
> **ANSWER: Document_Open**

#### Who is the author of the file "/root/Desktop/QuestionFiles/PO-465514-180820.doc"?  
> **ANSWER: Alexandre Riviere**

#### What is the last saved time of the "/root/Desktop/QuestionFiles/PO-465514-180820.doc" file?  
> **ANSWER: 2020-08-18 08:19:00**

#### The malicious file "/root/Desktop/QuestionFiles/Siparis_17.xls" is trying to download files from an address. From which domain is it trying to download the file?  
> **ANSWER: hocoso.mobi**

#### How many IOCs are in the "/root/Desktop/QuestionFiles/Siparis_17.xls" file according to the Olevba tool?  
> **ANSWER: 2**

---

# 5) Analysis with Sandboxes  
#### [Youtube Link](https://youtu.be/angOCPFG4P8)

## Lab  

```bash
Note: You can install Firefox on the Linux machine to upload the malicious file to Hybrid-Analysis,
or simply use the hash search feature on Hybrid-Analysis.
```

---

#### The file "/root/Desktop/QuestionFiles/PO-465514-180820.doc" is trying to make a request to a domain ending with ".kz". What is this domain?  
> **ANSWER: www.msbc.kz**

#### With which Windows tool are the connection requests made? (File: /root/Desktop/QuestionFiles/PO-465514-180820.doc)  
> **ANSWER: powershell.exe**

#### How many addresses does the file send DNS requests to? (File: /root/Desktop/QuestionFiles/PO-465514-180820.doc)  
> **ANSWER: 5**

#### The "/root/Desktop/QuestionFiles/Siparis_17.xls" malware document is trying to download a file. With what name does it want to save the file on the device?  
> **ANSWER: 6LeGwKmrm.jar**

---

# END