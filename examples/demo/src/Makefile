#makefile
#CC=gcc#mips-openwrt-linux-gcc
#FLAGS = -Wall
LDFLAGS := -lwilddog

objects = demo.o
demo : $(objects)
	$(CC) $(CFLAGS) -o demo $(objects) $(LDFLAGS) -static
	rm $(objects)
Wilddog_transfer.o files.o :

.PHONY : clean
clean :
	rm demo 	
