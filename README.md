# Finished-Project
from tkinter import *

#Creates root window, sets title, and positions window based on x and y coordinates, also sets width and height.
root = Tk()
root.title("Photo Editor")
root.geometry("1000x600+300+0")

#Creates menu widget and places its parent as the root window
menu = Menu(root)

#Create a file menu that will be a submenu of menu, add a open and save as to menu list.
file = Menu(menu,tearoff=0)
file.add_command(label="Open",command="")
file.add_command(label="Save as",command="")

#Function for when exit is clicked, closes root window.
def exit():
    root.quit()

#Set initial color of line to black.
default_color = "black"

#Select color function for when the select color menu option is clicked.
def select_color():
    #When confirm is clicked the default_color that is set to the color attribute in draw line is changed to the following values retrieved from entry in hexidecimal format.
    def confirm():
        global default_color
    
        red = value_red.get()
        green = value_green.get()
        blue = value_blue.get()

        value_red.set(red)
        value_green.set(green)
        value_blue.set(blue)

        color = '#%s%s%s' % (red,green,blue)
        
        default_color = color
        
        #Entry must be greater than zero for values to be changed.
        if(len(red)>0 and len(green)>0 and len(blue)>0):
            top.destroy()
        #If not greater than zero than pop up message tells user to enter values.
        else:
            top1 = Toplevel()
            label = Label(top1,text="Enter values into field.")
            label.grid(row=1,column=1)
            
            def destroy():
                top1.destroy()
            button = Button(top1,text="Ok",command=destroy)
            button.grid(row=2,column=1)
            
           

    #The following code is just the window, entry, and button widgets for the select color box.
    top = Toplevel()
    top_frame = Frame(top)
    top_frame.grid(column=1)
    top_frame.configure(width=200,height=200)

    value_red = StringVar()
    value_green = StringVar()
    value_blue = StringVar()
        
    label_red = Label(top_frame,text="Red")
    label_red.grid(row=0,column=0)
        
    entry_red = Entry(top_frame,textvariable=value_red)
    entry_red.grid(row=0,column=1)
    
    label_green = Label(top_frame,text="Green")
    label_green.grid(row=2,column=0)

    entry_green = Entry(top_frame,textvariable=value_green)
    entry_green.grid(row=2,column=1)

    label_blue = Label(top_frame,text="Blue")
    label_blue.grid(row=4,column=0)

    entry_blue = Entry(top_frame,textvariable=value_blue)
    entry_blue.grid(row=4,column=1)

    confirm_button = Button(top_frame,text="Confirm",command=confirm)
    confirm_button.grid(row=5,column=1)
        
#Removes shape items within canvas
def clear():
    canvas.delete('all')
    
#Add exit to file menu list.
file.add_command(label="Exit",command=exit)

#Edit menu is added to menu
edit = Menu(menu,tearoff=0)
edit.add_command(label="Select Color",command=select_color)
edit.add_command(label="Clear",command=clear)
menu.add_cascade(label="File",menu=file)
menu.add_cascade(label="Edit",menu=edit)

#Adds menu to root window.
root.config(menu=menu)

#Frame that will hold canvas widget.
canvas_frame = Frame(root)
canvas_frame.grid(row=1,column=2)

#Canvas widget
canvas = Canvas(canvas_frame,bg="white",width=900,height=500)
canvas.grid()

#Set initial x and y coordinates to 0 for line
last_x, last_y = 0,0

def set_xy(event):
    #Reference the variables in function
    global last_x,last_y
    #Set global equal to current mouse coordinates
    last_x,last_y = event.x,event.y

def draw_pen(event):
    #Reference changed global variables
    global last_x,last_y
    #Take set values for x1 and y1, then set x2 and y2 equal to current mouse coordinates
    canvas.create_line(last_x,last_y,event.x,event.y,fill=default_color)
    #Change the start coordinates to the end coordinates
    last_x,last_y = event.x, event.y

#Binds the left mouse button and when mouse button is held down to corresponding callback functions.
canvas.bind("<Button-1>",set_xy)
canvas.bind("<B1-Motion>",draw_pen)

#Frame that will contain tools in toolbar
button_frame = Frame(root)
button_frame.grid(row=1,column=0)

image_files = ["Button1.gif","Button2.gif","Button3.gif"]
cursor_images = []

#Button class for tools.
def create_buttons():
    global button_frame
    global image_files
    
    img1 = PhotoImage(file=image_files[0])
    button1 = Button(button_frame,image=img1)
    button1.image = img1
    button1.grid(row=0,column=0)
    
    img2 = PhotoImage(file=image_files[1])
    button2 = Button(button_frame,image=img2)
    button2.image = img2
    button2.grid(row=1,column=0)
    
    img3 = PhotoImage(file=image_files[2])
    button3 = Button(button_frame,image=img3)
    button3.image = img3
    button3.grid(row=2,column=0)
    
def change_cursor(event,img):
    cursor
#Creates instance of create_buttons class.
create_buttons()
root.mainloop()
