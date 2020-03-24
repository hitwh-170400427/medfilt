# medfilt
%matlab编程实现中值滤波
I=imread('c:/matlab/matlab2019a/noise.jpg');    
n=5; 

%matlab中值滤波器
I1 = padarray(I,[(n-1)/2,(n-1)/2]); %对图像边缘进行填充
K=medfilt2(I1,[n,n]);  %matlab中自带值滤波函数

figure;
imshow(K),title('中值滤波2'); 
