# Multi-threading and Multi-processing in Python

    import threading
    if __name__ == '__main__':
    	numberOfThreads = 5
    	threadList = []
    	for i in range(numberOfThreads):
    		t = threading.Thread(target = job,args = (arguments,))
    		t = start()
    		threadList.append(t)

    	print(threading.activeCount())

    	for i in range(numberOfThreads):
    		threadList[i].join()
    		# concatenate every thing together.




import multiprocessing as mp 

# similar
    p1 = mp.Process(target = job, args = (parameters,))
    p1.start()
    p1.join()


# Queue
# the job that will be used for multiprocessing should not return any value,
# we can put results in a queue, which whill be managed by the multiprocessing module

    def job(a,q):
    	print("somting")
    	# queue
    	q.put(a)

    import multiprocessing as mp 

    if __name__ == '__main__':
    	q = mp.Queue()
    	# similar
    	p1 = mp.Process(target = job, args = (a,q)) 
    	# if only one argument, need to do: args = (q,)
    	p1.start()
    	p1.join()
    	result = q.get()



# Pool
# 

    def multicore():
    	pool = mp.Pool(process = 4) # number of cores
    	res = pool.map(job, aListOfArgs)
    	# res is a list of results
    	# map automatically carry out multiprocessing for all the processes on multiple core
    	# something else
    	# res = pool.apply_asyc(job, (oneArg,))
    	# apply_asyc only one process.

# Share memory
    value = mp.Value('i',1)# 'i' integer 'd' double
# Now value can be used in multiple processes
    value.v += 1

#also we can do the same to share an array(list)
    array = mp.Array('i',[12,2,4]) # one dimension only

    l = mp.Lock()
    l.acquire()
    l.release()

