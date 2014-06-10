#include <stdio.h>	//headers for this program.
#include <string.h>
#include <stdlib.h>

#define Left(x) (2*(x) +1)	//definded for left right and parent nodes.
#define Right(x) (2*(x) + 2)
#define Parent(x) ((x) /2)

/*
*This builds the structure for the priority queue. It holds a size. A capacity, and the data we need to compare.
*
*/
typedef struct PQueueStruct 
{
size_t size; 
size_t capacity;
void **data;
int (*cmp) (const void *d1, const void *d2);
}priority_queue;


//Allocates a priority queue in memory
priority_queue *pq_create( int ( *cmp ) ( const void* element1, const void* element2 ),size_t capacity )
{
priority_queue *res = NULL;
res=malloc(sizeof(*res));
res->cmp = cmp;
res->data = malloc(capacity * sizeof(*(res->data)));
res->size = 0;
return(res);
}

//De-Allocates memory for the Priority Queue structure
void pqueue_destroy(priority_queue *q)
{
free(q->data);
free(q);
}

void pqueue_heapify(priority_queue *q, size_t idx) {
    /* left index, right index, largest */
    void *tmp = NULL;
    size_t l_idx, r_idx, lrg_idx;
    //NP_CHECK(q);

    l_idx = Left(idx);
    r_idx = Right(idx);

    /* Left child exists, compare left child with its parent */
    if (l_idx < q->size && q->cmp(q->data[l_idx], q->data[idx]) > 0) {
        lrg_idx = l_idx;
    } else {
        lrg_idx = idx;
    }
    /* Right child exists, compare right child with the largest element */
    if (r_idx < q->size && q->cmp(q->data[r_idx], q->data[lrg_idx]) > 0) {
        lrg_idx = r_idx;
    }


    /* At this point largest element was determined */
    if (lrg_idx != idx) {
        /* Swap between the index at the largest element */
        tmp = q->data[lrg_idx];
        q->data[lrg_idx] = q->data[idx];
        q->data[idx] = tmp;
        /* Heapify again */
        pqueue_heapify(q, lrg_idx);
    }
}

/*
*
*The pq_empty function takes a priority queue and if it is empty then the function returns 1. 
*If the queue is not empt then it returns 0.
*param q-a priority queue that is for a parameter.
*/
int pq_empty(priority_queue *q)
{
	if(q->size <= 0)
	{
	 return 1;
	}
	else
	{
	return 0;
	}
}

/*
*The pq_insert function takes a priority queue and data and then inserts it into the priority queue. 
*It is then compared with its parent and then the values are swapped until it is in the right order.
*@param q-a priority queue that is passed in, *data-data that is also passed in. 
*
*/
void pq_insert(priority_queue *q, const void *data)
{
	size_t i;
	void *tmp = NULL;

	q->data[q->size] = (void*) data;		//if the queue is not full then we add the element to the queue.
	i = q->size;
	q->size++;

	//new element is swapped with its parent
	while(i> 0 && q->cmp(q->data[i], q->data[Parent(i)]) >0)
	{
		tmp = q->data[i];
		q->data[i] = q->data[Parent(i)];
		q->data[Parent(i)] = tmp;
		i = Parent(i);
	}


}

/*
*
*the pq_max takes a priority queue and searches through the queue to find the max and return that value.
*@param- priority queue that is being searched.
*
*/
void *pq_max(priority_queue *q)
{
void *data = NULL;

	data = q->data[0];

	pqueue_heapify(q,0);
	return(data);



}

/*
*The pq_remove_max function takes a queue finds the max value and then removes it. Then it reorders the queue once it removes it.
*@param q-the priority queue that the top element is to be removed from.
*
*
*/
void *pq_Remove_max(priority_queue *q)
{
	void *data = NULL;
	if(q->size<1)
	{
	return NULL;    
	 }    
	data = q->data[0];
	q->data[0] = q->data[q->size-1];
	q->size--;
	pqueue_heapify(q,0);
	return(data);
}


/*
*The main funcion creates a series of priority queues and fills them up with data one at a time. It creates queues filled with various lengths that are to be compared and various strings. These are then compared,  sorted, and outputed.
*@param
*
*/
int main ()
{
int i;
	
	typedef struct word_cmp		//structure created to hold information for various words.
	{
	 char *str;
	 int count;
	}word;
	


	word word1, word2, word3;		//we are creating word1, word2, word3 here.
	word1.str="One";			//creates the word one as a string
	word1.count = 100;			//creates the count for word one as 100

	word2.str="Two";			//creates the string "Two" for the word2
	word2.count = 50;			//creates the count for word2 to be 50

	word3.str = "Three";			//creates the string "Three" for the word3
	word3.count = 20;			//creates the count for word3 to be 20

       
	/*
	*
	*The word_compare function takes two elements and compares them use the strcmp function.
	*strcmp retuns <0 if the second string is greater than the first string. 0 if the strings are equal.
	*and >0 if string2 is less than string one.
	*@param void d1- is the first element being passed in. void d2- is the second element being passed in
	*/
	int  word_compare(const void *d1, const void *d2)
	{
	  return strcmp(((word*)d1)->str, ((word*)d2)->str);

	}

	priority_queue* pq1 = pq_create(word_compare,3);		//creates a priority queue called pq1
	pq_insert(pq1, &word1);						//inserts the date into pq1
	pq_insert(pq1, &word2);						
	pq_insert(pq1, &word3);
	
	/*
	*
	*While the priority queue is not empty for pq1 then it prints out the max value in pq1 and then removes it.
	*However this is comparing strings in each word.
	*/
	printf("Test Case #1\n");
	while(!pq_empty(pq1))
	{
	 printf("%s\n", ((word*)pq_Remove_max(pq1))->str);

	}


	/*
	*
	*The count_compare method takes two elemnts and compares then to find which numbr is bigger. It then returns the largest number.
	*@param void d1- an element passed in to be compared. void d2- an element passed in to be compared.
	*/
	int count_compare(const void *d1, const void *d2)
	{
		return((word*)d1)->count - ((word*)d2)->count;
	}
	

	//This creates a new priority queue called pq2, and uses the count_compare function with 3 elemnts being passed in.
	priority_queue* pq2 = pq_create(count_compare,3);

	
	//inserts the elements into pq2. 
	pq_insert(pq2, &word1);
	pq_insert(pq2, &word2);
	pq_insert(pq2, &word3);
	printf("\nTest Case #2\n");
	
	/*
	*
	*While the pq2 is not empty it prints out the largest elements and removes it, but this time it is comparin how large
	*each eleent is and then prints out the words in the correct order based on how therir length.
	*
	*/
	while(!pq_empty(pq2))
	{
	printf("%s\n", ((word*)pq_Remove_max(pq2))->str); //prints max value in q
	}


	/*
	*
	*the number_cmp compares elements one and elements two that are being passed in. and then returns the largest number.
	*@param void d1- the first element being passed in, void d2- the second element being passed in.
	*
	*/
	int number_cmp(const void *d1, const void *d2)
	{
	  int i = *((int *) d1);
	  int j = *((int *) d2);
	  int c;
	  return (i>j) - (i <j);
	}

	//uses number comparator
	priority_queue* pq3 = pq_create(number_cmp, 5);

	/*
	*
	*Creates a for loop that passes the numbers one to five numbers into the pq3.
	*
	*/
	for(i = 1; i<=5; i++)
	{
		int* number = (int*) malloc(sizeof(int));
		*number = i;
		pq_insert(pq3, number);
	}
	

	printf("\nTest Case #3\n");
	printf("Max value in Test case #3 is: %d\n", *((int*) pq_max(pq3)));
	
	/*
	*
	*While pq3 is not empty it prints out the max element in pq3 and then removes it. 
	*
	*
	*/
	while(!pq_empty(pq3))
	{
		printf("%d\n", *((int*) pq_Remove_max(pq3)));
	}

pqueue_destroy(pq1);		//destorys each priority queue to deallocate the memory for it.
pqueue_destroy(pq2);
pqueue_destroy(pq3);


return 0;
}
