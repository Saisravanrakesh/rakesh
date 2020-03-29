#include<stdio.h> 
 
int main() 
{ 
      int i, lt, total = 0, x, count = 0, tm_qua,j; 
      
	  int wait_t = 0, turnarnd_t = 0,pos,z,p[10],prior[10], arrt[10], bu_t[10], temp[10],b; 
      
	  float av_w_t, av_tu_t;
      
	  printf("\nEnter Total Number of Processes:"); 
      
	  scanf("%d", &lt); 
      
	  x = lt; 
      for(i = 0; i < lt; i++) 
      {
	    p[i]=i+1;
	   
	    prior[i]=0;
            printf("\nEnter total Details of Process[%d]\n", i + 1);
            printf("Arrival Time:\t");
            scanf("%d", &arrt[i]);
            printf("Burst Time:\t");
            scanf("%d", &bu_t[i]); 
            temp[i] = bu_t[i];
      }
	   
      printf("\nEnter the Time Quantum:"); 
      scanf("%d", &tm_qua); 
      printf("\nProcess ID\t\tBurst Time\t Turnaround Time\t Waiting Time\t Priorrity\n");
      for(total = 0, i = 0; x != 0;) 
      { 

		    for(z=0;z<lt;z++)
		    {
			int temp1;
			pos=z;
			for(j=z+1;j<lt;j++)
			{
			    if(prior[j]<prior[pos])
				pos=j;
			}
		 
		temp1=prior[z];
	
		prior[z]=prior[pos];
	
		prior[pos]=temp1;
		 
			temp1=bu_t[z];
			bu_t[z]=bu_t[pos];
			bu_t[pos]=temp1;
		 			temp1=arrt[z];
				arrt[z]=arrt[pos];
			arrt[pos]=temp1;

			temp1=p[z];
				p[z]=p[pos];
			p[pos]=temp1;

			temp1=temp[z];
				temp[z]=temp[pos];
			temp[pos]=temp1;
		    }
		{
		}
            
			if(temp[i] <= tm_qua && temp[i] > 0) 
            { 
                  total = total + temp[i]; 
                  temp[i] = 0; 
                  count = 1; 
            } 
            
			else if(temp[i] > 0) 
            { 
                  temp[i] = temp[i] - tm_qua; 
                  total = total + tm_qua; 
            } 

	for(b=0;b<lt;b++)
		{
			if(b==i)
			prior[b]+=1;
			else
			prior[b]+=2;
		}

            if(temp[i] == 0 && count == 1) 
            { 
                  x--; 
                  printf("\nProcess[%d]\t\t%d\t\t %d\t\t %d\t\t%d", p[i], bu_t[i], total - arrt[i], total - arrt[i] - bu_t[i],prior[i]);
                  wait_t = wait_t + total - arrt[i] - bu_t[i]; 
                  turnarnd_t = turnarnd_t + total - arrt[i]; 
                  count = 0; 
            } 
            if(i == lt - 1) 
            {
                  i = 0; 
            
			}
            else if(arrt[i + 1] <= total) 
            {
                  i++;
            
			}
            else 
            {
                  i = 0;
            
			}		
      } 
      return 0; 

