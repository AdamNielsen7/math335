ggplot2 https://r4ds.had.co.nz/data-visualisation.html

ggplot(data = <DATA>) + 
  <GEOM_FUNCTION>(mapping = aes(<MAPPINGS>), aesthetic=value)

example: 
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy))
  
Aesthetics
color = class #changes the dots color based on categorical info
size = class
alpha # transparency
shape # max of 6

Facets #display subsets of data next to each other

facet_wrap # 1 variable
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy)) + 
  facet_wrap(~ class, nrow = 2)

facet_grid #2 variables
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy)) + 
  facet_grid(drv ~ cyl)
  
  
Geometric Objects
ggplot(data = mpg) + 
  geom_smooth(mapping = aes(x = displ, y = hwy, linetype = drv))
  
Combine graphs
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy)) +
  geom_smooth(mapping = aes(x = displ, y = hwy))

ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) + 
  geom_point(mapping = aes(color = class)) + 
  geom_smooth()
  

Bar Chart
ggplot(data = diamonds) + 
  geom_bar(mapping = aes(x = cut))
  
  
ggplot(data = <DATA>) + 
  <GEOM_FUNCTION>(
     mapping = aes(<MAPPINGS>),
     stat = <STAT>, 
     position = <POSITION>
  ) +
  <COORDINATE_FUNCTION> +
  <FACET_FUNCTION>