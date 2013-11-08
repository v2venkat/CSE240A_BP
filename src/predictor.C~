#include<stdio.h>
extern int ghr;
extern int weight_perceptron[32][32];
extern int y;
void init_predictor ()
{
	int i,j;
	ghr = 0;
	y = 0;
	for(i=0; i<32; i++)
	{
		for(j=0; j<32; j++)
		{
			weight_perceptron[i][j] = 0;
		}
	}
}

bool make_prediction (unsigned int pc)
{
	int i, j; /*i hashes into perceptron table. y is output of perceptron. */
	i = pc % 128;
	i = i / 4;
  	y = 0;
	for(j=0; j < 32; j++)
	{
		if(((ghr >> j) & 0x01))
		{
			y += weight_perceptron[i][j];
		}
		else
		{
			y -= weight_perceptron[i][j];
		}
	}
	
	if(y < 0) {return false;}
	else {return true;} 
}

void train_predictor (unsigned int pc, bool outcome)
{
	int i, j;
	i = pc % 128;
	i = i / 4;
	if((outcome == true))
	{

		//ghr = (ghr << 1) | 0x01;

		if(y < 0) {
		for(j = 0; j < 32; j++)
		{
			if(((ghr >> j) & 0x01))
			{	
				weight_perceptron[i][j] += 1;	
			}
			else{ weight_perceptron[i][j] -= 1; }	
		}
		}		
		ghr = (ghr << 1) | 0x01;
	}
	else { //ghr = (ghr << 1) & 0x00; 
			
	if(y >= 0) {		
	for(j = 0; j < 32; j++)
		{
			if(((ghr >> j) & 0x01) == 0)
			{	
				weight_perceptron[i][j] += 1;	
			}
			else{ weight_perceptron[i][j] -= 1; }	
		}		
		}	

		ghr = (ghr << 1) & 0x00;
	}

	
}
