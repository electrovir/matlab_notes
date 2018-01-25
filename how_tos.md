# MATLAB notes

A repo of my own MATLAB notes. It's not really organized, I mostly just cmd + f to find what I'm looking for anyway.

## Splitting script into sections

This allows you to write a single script but only run or print sections of it at a time. To run a single section, place the cursor within the section and click ``Editor`` > ``Run Section`` or, on a Mac, press ``cmd + return``.

Warning that this can make weird things happen. You'll have to run the script as a whole first before using any script-global variables. If you clear the memory anywhere in the section then those variables will be gone.

```MATLAB
%% My section 1
someCodeToDoStuff(1);
%% My section 2
% this can be run separately from section 1
someCodeToDoStuff(2);
```

## Matrices

**Indexing starts at 1.** Matrices and arrays are treated in the same ways. An array is just a matrix with one row.

### Define

```MATLAB
myMatrix = [1, 2, 3; 4, 5, 6]
```

Produces:

```
1 2 3
4 5 6
```

### Grab entire row

```MATLAB
myMatrix = [1, 2, 3; 4, 5, 6];
firstRow = myMatrix(1, :) % = [1, 2, 3]
```

### Grab entire column

```MATLAB
myMatrix = [1, 2, 3; 4, 5, 6];
firstColumn = myMatrix(:, 1) % = [1, 4]
```

### Size

```MATLAB
myMatrix = [1, 2, 3; 4, 5, 6];
size(myMatrix) % = [2, 3]
size(myMatrix, 1) % = 2
size(myMatrix, 2) % = 3
```

### Non-matrix multiply

Multiply each cell in matrix **a** with each cell of corresponding index in matrix **b**. This works with addition as well but the dot is not needed. Also works for exponents.

```MATLAB
a = [1, 2, 3];
b = [2, 4, 6];
a .* b % = [2, 8, 18]
```

## Plotting

### Plot to a figure

Simply call the figure with a number before calling plot.

```MATLAB
figure(1);
plot(x,y);
```

### Clear figure

```MATLAB
figure(1)
clf;
```

### Position figure

The x and y coords treat the bottom left corner of the screen as the origin (the screen is the first quadrant). x, y, w, h are just numbers.

```MATLAB
set(figure(1), 'position', [x, y, w, h])
```

### Plot bounds

```MATLAB
plot(x,y);
% x bounds from -1 to 1
xlim([-1, 1]);
% y bounds from -3 to 2
ylim([-3, 2]);
```

### Multiple plots

This will plot multiple lines on the same graph. They will also all be added to the legend (see later tips for making the legend appear and editing the names on it). This can be repeated as many times as needed.

```MATLAB
plot(x1,y1);
hold on;
plot(x2, y2);
```

### Line width

```MATLAB
plot(x, y, 'linewidth', 5);
```

### Marker/point size

```MATLAB
plot(x,y, 'markersize', 6);
```

### Marker/point type/symbol

Replace the 'o' with the symbol you want. [online spec](https://www.mathworks.com/help/matlab/ref/linespec.html)

```MATLAB
plot(x, y, 'o');
```

### Line color

Can be a color name (limited names) or other way of specifying a color. [online spec](https://www.mathworks.com/help/matlab/ref/colorspec.html)

```MATLAB
plot(x, y, 'color', 'green');
```

### Legend labels

```MATLAB
plot(x1, y1, 'displayname', 'plot1');
plot(x2, y2, 'displayname', 'plot2');

legend(gca,'show');
```

### Plot labels

```MATLAB
plot(x,y);
xlabel('X-axis label');
ylabel('Y-axis label');
title('Plot title');

subplot(2, 1, 1);
suptitle('Super title for sub plots'); % this typically looks really ugly
```

### Sub plots

```MATLAB
% two plots, 2 vertical 1 horizontal
% first plot
subplot(2,1,1);
plot(x1,y1);
% second plot
subplot(2,1,2);
```

### Inline functions

This allows you to make a one-line function anywhere in a script file.

```MATLAB
name = @(input, list) (calculation);
```

### Functions in a script

A complete function definition can be included in a script file is it is placed at the very end of the file. This doesn't work when your script is broken up into sections and you're only running a single section at a time.

```MATLAB
myScript = doStuff(3);

function output = doStuff(whatever)
  output = 3+2;
end
```
### Number in title

Include a variable in a string for a title or legend, etc.

```MATLAB
title(['title for iteration ', num2str(index)])
```

### Plot label sizes

```MATLAB
plot(x,y);
xlabel('x', 'fontsize', 14);
ylabel('y', 'fontsize', 14);
title('plot title', 'fontsize', 16);
% now you can actually read your labels!
% would be nice to know how to do this for legends as well...
```