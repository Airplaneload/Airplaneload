clear;
clc;
data=xlsread('948data.xlsx','test');

x=data(:,1);
y=data(:,2);
z=data(:,3);

plot3(x,y,z, 'o');
hold on;
%拟合
VOX=0;
VOY=0;
VOZ=0;
VRX=0;
VRY=0;
VRZ=0;
Y=-x.*x;
A=ones(length(x),1);
K=[y.*y z.*z x y z A]; 

X=inv(K'*K)*K'*Y;
VOX=-X(3,1)/2;
VOY=-X(4,1)/2/X(1,1);
VOZ=-X(5,1)/2/X(2,1);
VRX=sqrt(VOX*VOX+X(1,1)*VOY*VOY+X(2,1)*VOZ*VOZ-X(6,1));
VRY=sqrt(VRX*VRX/X(1,1));
VRZ=sqrt(VRX*VRX/X(2,1));


%显示拟合曲面
[x1, y1, z1] = ellipsoid(VOX, VOY, VOZ, VRX, VRY, VRZ, 100);  
plot3(x1, y1, z1);  
hold on;

x2=(x-VOX);
y2=(y-VOY)*VRX/VRY;
z2=(z-VOZ)*VRX/VRZ;                                 
plot3(x2, y2, z2,'o');  
hold on;
k_pitch=10/57.3;
k_roll=0/57.3;
mZx = cos(k_pitch) * x2 + sin(k_pitch) * sin(k_roll) * y2 + sin(k_pitch) * cos(k_roll) * z2;
mZy = cos(k_roll) * y2 - sin(k_roll) * z2;
mZz = -sin(k_pitch) * x2 + cos(k_pitch) * sin(k_roll) * y2 + cos(k_pitch) * cos(k_roll) * z2;
%plot3(mZx, mZy, mZz,'o');  
%hold on;

%显示拟合曲面
[x3, y3, z3] = ellipsoid(0, 0, 0, VRX,  VRX,  VRX, 30);  
plot3(x3, y3, z3)

grid on;
axis equal;
xlabel('X');
ylabel('Y');
zlabel('Z');
