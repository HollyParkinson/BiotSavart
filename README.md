# BiotSavart
Python code to implement the Biot-Savart law for a given length or coil of wire, provided said wire is constructed of straight lines between points.

#import relevant modules
import numpy
import matplotlib.pyplot as plt
import scipy

I = 20 #Current / A
mu0 = 4*numpy.pi*1e-7 #Vacuum permeability / H/m
k = mu0/(4*numpy.pi) #Constant

wire = [(0,0,0),(1,0,0),(1,1,0),(0,1,0)] #vertex coordinates of square coil loop
x = 5
y = 5
z = 0

#(can be replaced with other coordinates provided that they are joined by straight lines to make the wire/loop) 



#function for the vector (Bx, By, Bz) at a given point

def Bfield(x,y,z):
    for i in range(len(wire)): #decrease range by 1 if doing a line, not a loop
        dlx = wire[i][0]-wire[i-1][0] #x-component of wire element vector
        dly = wire[i][1]-wire[i-1][1] #y-component """"""
        dlz = wire[i][2]-wire[i-1][2] #z-component """"""
        dl = [dlx,dly,dlz] 
        displacement_x = x - (wire[i][0]+dlx) #x-component of displacement vector from given point to wire element
        displacement_y = y - (wire[i][1]+dly) #y-component """"""
        displacement_z = z - (wire[i][2]+dlz) #z-component """"""
        displacementvec = numpy.array([displacement_x, displacement_y, displacement_z])
        mag_r = (displacement_x**2 + displacement_y**2 + displacement_z**2)**0.5 #magnitude of displacement vector
        a = k*I*numpy.cross(dl, displacementvec) / mag_r**3 #implements Biot-Savart equation to give (Bx, By, Bz)
        return a


#function for the magnitude of the B-field at a given point

def Bfield_Mag(x,y,z):
    for i in range(len(wire)):
        dlx = wire[i][0]-wire[i-1][0]
        dly = wire[i][1]-wire[i-1][1]
        dlz = wire[i][2]-wire[i-1][2]
        dl = [dlx,dly,dlz]
        displacement_x = x - (wire[i][0]+dlx)
        displacement_y = y - (wire[i][1]+dly)
        displacement_z = z - (wire[i][2]+dlz)
        displacementvec = [displacement_x, displacement_y, displacement_z]
        mag_r = (displacement_x**2 + displacement_y**2 + displacement_z**2)**0.5
        a = k*I*numpy.cross(dl, displacementvec)/mag_r**3 
        print(a)
        b = (a[0]**2 + a[1]**2 + a[2]**2)**0.5 #finds magnitude of (Bx, By, Bz)
        return b


"""Function test for single (x,y,z)"""

x = 5
y = 5
z = 0

print("(Bx, By, Bz) =" , "(",Bfield(x,y,z)[0], "," ,Bfield(x,y,z)[1], "," , Bfield(x,y,z)[2], ")")
print("|B| =", Bfield_Mag(x,y,z), "T")

def Bplot(x,y,z):
    result = numpy.zeros((len(x),3))
    for i in range(len(wire)):
        dlx = wire[i][0]-wire[i-1][0]
        dly = wire[i][1]-wire[i-1][1]
        dlz = wire[i][2]-wire[i-1][2]
        dl = [dlx,dly,dlz]
        displacement_x = numpy.zeros([len(x)])
        displacement_y = numpy.zeros([len(x)])
        displacement_z = numpy.zeros([len(x)])
        for j in range(len(x)):
                displacement_x[j] = x[j] - (wire[i][0]+dlx)
                displacement_y[j] = y[j] - (wire[i][1]+dly)
                displacement_z[j] = z[j] - (wire[i][2]+dlz)
                displacementvec = [displacement_x[j], displacement_y[j], displacement_z[j]]
                mag_r = (displacement_x[j]**2 + displacement_y[j]**2 + displacement_z[j]**2)**0.5
                a = k*I*numpy.cross(dl, displacementvec)/mag_r**3 #a = B field at one point due to one coil
                result[j,0] += a[0]
                result[j,1] += a[1]
                result[j,2] += a[2]
          
    return result


#add another coil (Helmhotlz setup with specific spacing)

I_1 = 20 #Current / A in coil 1
mu0 = 4*numpy.pi*1e-7 #Vacuum permeability / H/m
k = mu0/(4*numpy.pi) #Constant
wire_1 = [(-1.5,-1.5,-0.81675),(1.5,-1.5,-0.81675),(1.5,1.5,-0.81675),(-1.5,1.5,-0.81675)] #vertex coordinates of square coil 1


I_2 = 20 #Current / A in coil 2
mu0 = 4*numpy.pi*1e-7 #Vacuum permeability / H/m
k = mu0/(4*numpy.pi) #Constant
wire_2 = [(-1.5,-1.5,0.81675),(1.5,-1.5,0.81675),(1.5,1.5,0.81675),(-1.5,1.5,0.81675)] #vertex coordinates of square coil 2

x = numpy.linspace(-5,5,1000) #x-coordinate of given point
y = numpy.linspace(-5,5,1000) #y-coordinate """"""
z = numpy.linspace(-5,5,1000) #z-coordinate """"""

#add another coil (Helmhotlz setup with specific spacing)

I_1 = 20 #Current / A in coil 1
mu0 = 4*numpy.pi*1e-7 #Vacuum permeability / H/m
k = mu0/(4*numpy.pi) #Constant
wire_1 = [(-1.5,-1.5,-0.81675),(1.5,-1.5,-0.81675),(1.5,1.5,-0.81675),(-1.5,1.5,-0.81675)] #vertex coordinates of square coil 1


I_2 = 20 #Current / A in coil 2
mu0 = 4*numpy.pi*1e-7 #Vacuum permeability / H/m
k = mu0/(4*numpy.pi) #Constant
wire_2 = [(-1.5,-1.5,0.81675),(1.5,-1.5,0.81675),(1.5,1.5,0.81675),(-1.5,1.5,0.81675)] #vertex coordinates of square coil 2

x = numpy.linspace(-5,5,1000) #x-coordinate of given point
y = numpy.linspace(-5,5,1000) #y-coordinate """"""
z = numpy.linspace(-5,5,1000) #z-coordinate """"""


