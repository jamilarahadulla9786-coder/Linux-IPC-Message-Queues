# Linux-IPC-Message-Queues
Linux IPC-Message Queues

# AIM:
To write a C program that receives a message from message queue and display them

# DESIGN STEPS:

### Step 1:

Navigate to any Linux environment installed on the system or installed inside a virtual environment like virtual box/vmware or online linux JSLinux (https://bellard.org/jslinux/vm.html?url=alpine-x86.cfg&mem=192) or docker.

### Step 2:

Write the C Program using Linux message queues API 

### Step 3:

Execute the C Program for the desired output. 

# PROGRAM:

## C program that receives a message from message queue and display them
```
#include <stdio.h> 
#include <sys/ipc.h> 
#include <sys/msg.h> 
#include <string.h>
#include <stdlib.h>
// structure for message queue 
struct mesg_buffer { 
	long mesg_type; 
	char mesg_text[100]; 
} message; 
int main() 
{ 	key_t key; 
	int msgid; 

	key = ftok("progfile", 65); 


	msgid = msgget(key, 0666 | IPC_CREAT); 
	message.mesg_type = 1; 
	printf("Write Data : "); 
scanf("%s",message.mesg_text);

	msgsnd(msgid, &message, sizeof(message), 0); 

	printf("Data send is : %s \n", message.mesg_text); 
	return 0; 
} 


// C Program for Message Queue (reader Process) 

#include <stdio.h>
#include <sys/ipc.h>
#include <sys/msg.h>

// structure for message queue
struct mesg_buffer {
	long mesg_type;
	char mesg_text[100];
} message;
int main()
{
	key_t key;
	int msgid;
// ftok to generate unique key
	key = ftok("progfile", 65);
	// msgget creates a message queue
	// and returns identifier
	msgid = msgget(key, 0666 | IPC_CREAT);
	// msgrcv to receive message
	msgrcv(msgid, &message, sizeof(message), 1, 0);
	// display the message
	printf("Data Received is : %s \n",
			message.mesg_text);

	// to destroy the message queue
	msgctl(msgid, IPC_RMID, NULL);
	return 0;
}
```





## OUTPUT
file:///home/rahman/os/ex04/Linux-IPC-Message-Queues/img4/04.png<img width="800" height="669" alt="image" src="https://github.com/user-attachments/assets/d2be2f04-946f-484c-ae3e-11d0f9e5f462" />
file:///home/rahman/os/ex04/Linux-IPC-Message-Queues/img4/Screenshot%20at%202026-03-19%2018-35-33.png<img width="771" height="597" alt="image" src="https://github.com/user-attachments/assets/1763742a-3e13-4dee-8ea6-0c000b625d32" />
file:///home/rahman/os/ex04/Linux-IPC-Message-Queues/img4/Screenshot%20at%202026-03-19%2018-36-12.png<img width="794" height="671" alt="image" src="https://github.com/user-attachments/assets/6c7a4771-5c93-4743-a335-f3a55c37153d" />
file:///home/rahman/os/ex04/Linux-IPC-Message-Queues/img4/Screenshot%20at%202026-03-19%2018-38-00.png<img width="807" height="267" alt="image" src="https://github.com/user-attachments/assets/00c88db5-eb3a-4df8-808c-2b1cc54fefec" />







# RESULT:
The programs are executed successfully.
