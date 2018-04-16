#include<iostream>
#include<conio.h>
 
#define n 4
 
using namespace std;
 
int compltedPhilo = 0,i;
 
struct fork{
    int taken;
}ForkAvil[n];
 
struct philosp{
    int left;
    int right;
}Philostatus[n];
 
void goForDinner(int philID){ 
    if(Philostatus[philID].left==10 && Philostatus[philID].right==10)
        cout<<"student "<<philID+1<<" question paper\n";
    
    else if(Philostatus[philID].left==1 && Philostatus[philID].right==1){
            
            cout<<"student "<<philID+1<<"question paper\n";
 
            Philostatus[philID].left = Philostatus[philID].right = 10; 
            int otherFork = philID-1;
 
            if(otherFork== -1)
                otherFork=(n-1);
 
            ForkAvil[philID].taken = ForkAvil[otherFork].taken = 0; 
            cout<<"student "<<philID+1<<" released paper "<<philID+1<<" and paper "<<otherFork+1<<"\n";
            compltedPhilo++;
        }
        else if(Philostatus[philID].left==1 && Philostatus[philID].right==0){
                if(philID==(n-1)){
                    if(ForkAvil[philID].taken==0){
                        ForkAvil[philID].taken = Philostatus[philID].right = 1;
                        cout<<"paper"<<philID+1<<" taken by student "<<philID+1<<"\n";
                    }else{
                        cout<<"student "<<philID+1<<" is waiting for paper "<<philID+1<<"\n";
                    }
                }else{
                    int dupphilID = philID;
                    philID-=1;
 
                    if(philID== -1)
                        philID=(n-1);
 
                    if(ForkAvil[philID].taken == 0){
                        ForkAvil[philID].taken = Philostatus[dupphilID].right = 1;
                        cout<<"paper "<<philID+1<<" taken by student "<<dupphilID+1<<"\n";
                    }else{
                        cout<<"student"<<dupphilID+1<<" is waiting for paper "<<philID+1<<"\n";
                    }
                }
            }
            else if(Philostatus[philID].left==0){
                    if(philID==(n-1)){
                        if(ForkAvil[philID-1].taken==0){
                            ForkAvil[philID-1].taken = Philostatus[philID].left = 1;
                            cout<<"paper "<<philID<<" taken by student "<<philID+1<<"\n";
                        }else{
                            cout<<"student "<<philID+1<<" is waiting for paper "<<philID<<"\n";
                        }
                    }else{
                        if(ForkAvil[philID].taken == 0){
                            ForkAvil[philID].taken = Philostatus[philID].left = 1;
                            cout<<"paper "<<philID+1<<" taken by student "<<philID+1<<"\n";
                        }else{
                            cout<<"student"<<philID+1<<" is waiting for paper "<<philID+1<<"\n";
                        }
                    }
        }else{}
} 
int main(){
    for(i=0;i<n;i++)
        ForkAvil[i].taken=Philostatus[i].left=Philostatus[i].right=0;
 
    while(compltedPhilo<n){

        for(i=0;i<n;i++)
            goForDinner(i);
        cout<<"\nTill now num of student completed question paper are "<<compltedPhilo<<"\n\n";
    }
 
    return 0;
}
