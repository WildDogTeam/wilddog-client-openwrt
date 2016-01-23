#makefile
#wilddog sdk used pthread in tinydtls, so if using tinydtls, we must add pthread lib
LDFLAGS := -lwilddog -lpthread

objects = demo.o
demo : $(objects)
	$(CC) $(CFLAGS) -o demo $(objects) $(LDFLAGS) -static
	rm $(objects)

.PHONY : clean
clean :
	rm demo 	
