# ChemE-5440-PS3

## a) 
*Note*: All arrays are listed in [Array.xlsx](https://github.com/lenareeb/ChemE-5440-PS3/blob/master/PS3/Arrays.xlsx) (which contains labeled rows and columns) and each array also has its own csv file.

The stoichiometric array S ([Stoichiometric_array(S).csv](https://github.com/lenareeb/ChemE-5440-PS3/blob/master/PS3/Stoichiometric_array(S).csv)) was constructed in Excel using KEGG

## b) 
Atomic array A ([Atomic_array(A).csv](https://github.com/lenareeb/ChemE-5440-PS3/blob/master/PS3/Atomic_array(A).csv)) was constructed in Excel using KEGG, which contains elementally balances around C,H,N,O,P, and S.

The command **using CSV** was used so that the csv files could be imported into Julia.
All arrays were imported and assigned to a variable following the following command:
**S=Matrix(CSV.read("Stoichiometric_array(S).csv";header=0))**

Elemental balance for the Urea cycle was verified via matrix multiplication: **E=A’S**

## c)
The flux bound array ([Flux_bounds_array(Lv,Uv).csv](https://github.com/lenareeb/ChemE-5440-PS3/blob/master/PS3/Flux_bounds_array(Lv%2CUv).csv)) was generated. The lower bounds of the fluxes for the reaction terms were 0. The upper bounds were calculated as **(v_max)saturation_term(s)**, where the saturation terms are in the form of **(S/(S+K_m))**. The saturation terms were generated for the reactants from data from *BRENDA* and *Park et al Nat Chem Biol 12:482-9, 2016*. For K_m, when there was a range, the K_m used was an average of the upper and lower bounds of the range. Where reactant species data was not available, the saturation terms were neglected.

The flux bounds and species bounds matrices ([Species_bounds_array(Lx,Ux).csv](https://github.com/lenareeb/ChemE-5440-PS3/blob/master/PS3/Species_bounds_array(Lx%2CUx).csv)) were imported using the above syntax. The vector holding indexes for the objective function ([Indexes_array(c).csv](https://github.com/lenareeb/ChemE-5440-PS3/blob/master/PS3/Indexes_array(c).csv)) was assigned as such: **c=vec(Matrix(CSV.read("Indexes_array(c).csv";header=0)))**

By including [Flux.jl](https://github.com/lenareeb/ChemE-5440-PS3/blob/master/PS3/Kegg-master/src/Include.jl), **calculate_optimal_flux_distribution** was run using the above specified inputs. 

*Note*: The saturation coefficient for L-arginine significantly changed the upper flux bound for reaction v3 (EC:3.5.3.1).
