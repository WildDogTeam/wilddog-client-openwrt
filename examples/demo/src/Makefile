#makefile

LDFLAGS := -lwilddog -lpthread

objects = demo.o
demo : $(objects)
	$(CC) $(CFLAGS) -o demo $(objects) $(LDFLAGS) -static
	rm $(objects)

.PHONY : clean
clean :
	rm demo 	
