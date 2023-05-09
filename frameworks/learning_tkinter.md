# Learning Tkinter

## Introduction

Tkinter is a Python interface to the Tk GUI library and has been a part of the Python standard library since 1994 with the release of Python version 1.1, making it the de-facto GUI library for Python.

Installing `tkinter`,

```bash
sudo pacman -S tk
```

Simple `Hello World!` program in `tkinter`,

```python
"""Hello world in tkinter"""
import tkinter as tk

# Every Tkinter program must have exactly one root window, which represents both
# the top-level window of our application, and the application itself.
# The root window is an instance of the Tk class.

root = tk.Tk()

label = tk.Label(root, text="Hello world!!")

# This is a Label widget, which is just a panel that can display some text.
# The first argument to any Tkinter widget is always the parent widget (sometimes called
# master widget); in this case, we've passed in a reference to our root window. The
# parent widget is the widget on which our Label will be placed, so this Label will
# be directly on the root window of the application.

label.pack()

# The pack() method of the Label widget is called a geometry manager method. Its job
# is to determine how the widget will be attached to its parent widget, and to draw it
# there.

root.mainloop()

# This line starts our application's event loop. The event loop is an infinite loop that
# continually processes any events that happen during the execution of the program.

```

### A Tkinter Program

```python
import tkinter as tk

root = tk.Tk()

root.title("Programming Languages")

root.geometry('640x480+300+300')
root.resizable(False, False)

# Create The Widgets

title = tk.Label(root, text="Programming Languages",
                 font=('Ariel 16 bold'), bg='brown', fg='#FF0')

name_label = tk.Label(root, text="What is your name?")
name_input = tk.Entry(root)

checkbox_input = tk.Checkbutton(root, text='Check this out, this is a checkbox in tkinter')

number_label = tk.Label(root, text='Choose the number of languages from here,')
number_input = tk.Spinbox(root, from_=0, to=100, increment=1)

list_label = tk.Label(root, text='Here is the list, choose your favorite language,')
list_input = tk.Listbox(root, height=1)

list_choices = ('Any', 'C', 'Python', 'JavaScript')

for choice in list_choices:
    list_input.insert(tk.END, choice)

radio_label = tk.Label(root, text='This is a radioButton in tkinter,')
radio_frame = tk.Frame(root)
radio_yes = tk.Radiobutton(radio_frame, text='Yes')
radio_no = tk.Radiobutton(radio_frame, text='No')

large_text_label = tk.Label(root, text='Explain about your programming journey?,')
large_text_input = tk.Text(root, height=3)

submit_btn = tk.Button(root, text='click here, to submit.')


output_label = tk.Label(root, text='', anchor='w', justify='left')

# Placing The Widgets On Window

name_label.grid(row=1, column=0)
name_input.grid(row=1, column=1)

title.grid(columnspan=2)

checkbox_input.grid(row=2, columnspan=2, sticky='we')

number_label.grid(row=3, sticky=tk.W)
number_input.grid(row=3, column=1, sticky=(tk.W + tk.E))

list_label.grid(row=4, columnspan=2, sticky=tk.W, pady=10)
list_input.grid(row=5, columnspan=2, sticky=(tk.W + tk.E), padx=25)

radio_yes.pack(side='left', fill='x', ipadx=10, ipady=5)
radio_no.pack(side='left', fill='x', ipadx=10, ipady=5)
radio_label.grid(row=6, columnspan=2, sticky=tk.W)
radio_frame.grid(row=7, columnspan=2, sticky=tk.W)

large_text_label.grid(row=8, sticky=tk.W)
large_text_input.grid(row=9, columnspan=2, sticky='NSEW')
submit_btn.grid(row=99)
output_label.grid(row=100, columnspan=2, sticky='NSEW')

root.columnconfigure(1, weight=1)
root.rowconfigure(99, weight=2)
root.rowconfigure(100, weight=1)

# Callback Function

def on_submit():
    name = name_input.get()
    number = number_input.get()

    selected = list_input.curselection()

    if selected:
        list_item = list_input.get(selected)
    else:
        list_item = ''

    text_data = large_text_input.get('1.0', tk.END)

    message = (f'Hello {name}, this is generated from tkinter, So you know{number} programming languages, and your favorite one is {list_item}.')
    output_label.configure(text=message)
    print(text_data)


submit_btn.configure(command=on_submit)

# MainLoop

root.mainloop()
```

### Handling data

`Tkinter Control Variables` are special tkinter objects that allow us to store data, these are,

- `StringVar`,
- `IntVar`,
- `DoubleVar`,
- `BooleanVar`

```python
name_var = tk.StringVar(root)
name_label = tk.Label(root, text='What is your name?')
name_inp = tk.Entry(root, textvariable=name_var)
```
