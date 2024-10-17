#  Project=3 	ʕ •̀ o •́ ʔ

# Problem 1 (5 pts):
Write a script (or Jupyter Notebook code block) that opens the file, uses a for loop to read through the file line by line and, after finishing reading through the file, reports the highest water level and the date and time that was observed.




file_path = 'CO-OPS__8729108__wl.csv'
max_level = float('-inf') 
max_date_time = ""
with open(file_path, 'r') as file:
    for line in file:
        parts = line.strip().split(',')
        if len(parts) >= 2:
            date_time = parts[0]  
            level_str = parts[1]  
            try:
                level = float(level_str)
            except ValueError:   
                continue 
            if level > max_level:
                max_level = level
                max_date_time = date_time
if max_date_time:
    print(f"The highest water level was {max_level} observed on {max_date_time}.")
else:
    print("No valid water level data found.")

  #  Problem 2 (5 pts):
Either in a new script or modifying the above script, calculate the lowest, highest and average water level observed during the time period. As above, print the date and time for the lowest and highest readings. 


file_path = 'CO-OPS__8729108__wl.csv'
max_level = float('-inf')  
min_level = float('inf')  
max_date_time = ""
min_date_time = ""

total_level = 0
count = 0
with open(file_path, 'r') as file:
    for line in file:  
        parts = line.strip().split(',')
        if len(parts) >= 2:
            date_time = parts[0]  
            level_str = parts[1] 
            
            try:
                level = float(level_str)
            except ValueError:   
                continue
            total_level += level
            count += 1

            if level > max_level:
                max_level = level
                max_date_time = date_time

            if level < min_level:
                min_level = level
                min_date_time = date_time
average_level = total_level / count if count != 0 else 0
if count > 0:
    print(f"The highest water level was {max_level} observed on {max_date_time}.")
    print(f"The lowest water level was {min_level} observed on {min_date_time}.")
    print(f"The average water level during the period was {average_level:.2f}.")
else:
    print("No valid water level data found.")

# Problem 3 (5 pts):
Write a script (or Jupyter Notebook) that calculates the fastest rise in water level per 6-minute period between measurements (for this assignment, assume that each line of the dataset is a 6-minute interval) and reports the date and time that was observed and the change in water level from the previous recording.

file_path = 'CO-OPS__8729108__wl.csv'
max_rise = float('-inf')  
max_rise_date_time = ""
previous_level = None  
previous_date_time = "" 

with open(file_path, 'r') as file:
    for line in file:
        parts = line.strip().split(',')
        
        if len(parts) >= 2:
            date_time = parts[0]  
            level_str = parts[1]  
            
            try:
                current_level = float(level_str)
            except ValueError:
                continue

            if previous_level is not None:
                rise = current_level - previous_level   
                if rise > max_rise:
                    max_rise = rise
                    max_rise_date_time = date_time

            previous_level = current_level
            previous_date_time = date_time

if max_rise_date_time:
    print(f"The fastest rise in water level was {max_rise:.2f} units observed on {max_rise_date_time}.")
else:
    print("No valid water level data found to calculate the rise.")
    
# Problem 4 (5 pts):
Imagine that the file is providing live readings of the water level. Write a script (or Jupyter Notebook) to print a line of text with a warning if any of these events occur:

The water level increases more than 0.25 since the previous recording.
The water level is over 5.0.
No reading is received at a time point.

file_path = 'CO-OPS__8729108__wl.csv'
previous_level = None  
previous_date_time = ""
with open(file_path, 'r') as file:
    for line in file:
        parts = line.strip().split(',')
        
        if len(parts) == 0 or len(parts[1].strip()) == 0:
            print(f"Warning: No reading received at {previous_date_time}.")
            continue
        if len(parts) >= 2:
            date_time = parts[0]  
            level_str = parts[1]  
            try:
                current_level = float(level_str)
            except ValueError:
                print(f"Warning: Invalid water level data at {date_time}.")
                continue
            # 5.0
            if current_level > 5.0:
                print(f"Warning: Water level over 5.0 units at {date_time}, current level: {current_level}.")
            # previous water level
            if previous_level is not None:
                rise = current_level - previous_level     
                # 0.25
                if rise > 0.25:
                    print(f"Warning: Water level increased by more than 0.25 units at {date_time}, rise: {rise}.")
            # Update the previous level and date/time for the next iteration
            previous_level = current_level
            previous_date_time = date_time



