Avantgarde module system does not dependent on directory layout. You should feel free to put components in any place you like.
You might think about chaotic project structure in this case. This proposal intended to study Haskell(BackPack), Ocaml high level module system to make modules rock-solid and flexible.


Backpack:
  Experience, description.
  
Ocaml:
  Experience, description.
  
  
Requiremenets:
  - Module system should provide transparent way of loading dependencies.
  - Module system should not tie components to file system (though some recommended file structure might be possible).
  - Module system should fulfill the role of IOC container used in many object-oriented languages
