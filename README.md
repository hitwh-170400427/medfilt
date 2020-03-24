 
I=imread('c:/matlab/matlab2019a/noise.jpg');    
n=5; 
%对图像边缘进行填充
[M,N]=size(I);
M1=M+n-1;
N1=N+n-1;
J=zeros(M1,N1);
%中
for i=1:M
    for j=1:N
        J(i+(n-1)/2,j+(n-1)/2)=I(i,j);
    end
end
%上
for i=1:(n-1)/2
    for j=1+(n-1)/2:N+(n-1)/2
        J(i,j)=I(1,j-(n-1)/2);
    end
end
%下
for i=1+(n-1)/2+M:M+n-1
    for j=1+(n-1)/2:N+(n-1)/2
        J(i,j)=I(M,j-(n-1)/2);
    end
end
%左
for i=1:M+n-1
    for j=1:(n-1)/2
        J(i,j)=J(i,1+(n-1)/2);
    end
end
%右
for i=1:M+n-1
    for j=1+N+(n-1)/2:N+n-1
        J(i,j)=J(i,N+(n-1)/2);
    end
end
%中值滤波
for i=1:M1-n+1  
    for j=1:N1-n+1  
        nn=J(i:i+(n-1),j:j+(n-1)); %提取n*n矩阵
        a=reshape(nn,1,n*n);%将n*n矩阵转换为1*n^2矩阵
%         a=nn(1,:);     
%         for k=2:n  
%             a=[a,nn(k,:)];          
%         end  
        med=median(a);      %取中值  
        J(i+(n-1)/2,j+(n-1)/2)=med;   %将模板元素中值赋给模板中心元素  
    end  
end    
J=uint8(J);%double型转uint8型

%matlab中值滤波器
I1 = padarray(I,[(n-1)/2,(n-1)/2]); %对图像边缘进行填充
K=medfilt2(I1,[n,n]);  %matlab中自带值滤波函数

figure;
subplot(131),imshow(I),title('原图');
subplot(132),imshow(J),title('中值滤波1');  
subplot(133),imshow(K),title('中值滤波2'); 
