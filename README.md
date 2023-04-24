# Código gerado para o projeto de iniciação cientifica
#### ESTUDO E APLICAÇÃO DE VERIFICAÇÃO DE MODELOS EM FUNÇÕES VEICULARES MODELADAS EM ESTADOS FINITOS
Link do Artigo: https://sistemas.bambui.ifmg.edu.br/open_conference/index.php/sic/sic2022/paper/viewFile/610/298

Sistema feito utilizando Verificação formal utilizando o método Modelar, Especificar e Verificar:
 - Sendo utilizado para modelar a ferramenta Stateflow do Software Matlab/Simulink
 - Para especificar foi utilizando a Lógica Temporal
 - Para verificar foi utilizado software de Verificação de Modelos NuSMV escrito no padrão da linguagem SMV

### Especificação da função veicular Cruise Control Management, Utilizando Lógica temporal
----------------------------------------------VVehicle-----------------------------------------

SCGND e SCVBAT
- Se (VVehicle > 30 | VVehicle < 180) & SCGND & SCVBAT = TRUE, então VVehicle = VehicleSpeed
- Se VVehicle = 30 & SCGND & SCVBAT = TRUE, então VVehicle = VehicleSpeed
- Se VVehicle = 180 & SCGND & SCVBAT = TRUE, então VVehicle = VehicleSpeed
- Se !CCL & SCGND & SCVBAT = TRUE, então VVehicle = VehicleSpeed

ClutchSwitch e BrakePedalSts
- Se (VVehicle > 30 | VVehicle < 180) ClutchSwitch & BrakePedalSts = TRUE, então VVehicle = VehicleSpeed
- Se VVehicle = 30 & ClutchSwitch & BrakePedalSts = TRUE, então VVehicle = VehicleSpeed
- Se VVehicle = 180 & ClutchSwitch & BrakePedalSts = TRUE, então VVehicle = VehicleSpeed
- Se !CCL & ClutchSwitch & BrakePedalSts = TRUE, então VVehicle = VehicleSpeed

UP
- Se (VVehicle > 30 | VVehicle < 180) & UP = TRUE, então VVehicle = VVehicle++
- Se VVehicle = 30 & UP = TRUE, então VVehicle = VVehicle++
- Se VVehicle = 180 & UP = TRUE, então VVehicle = VVehicle
- Se !CCL & UP = TRUE, então VVehicle = VehicleSpeed

DOWN
- Se (VVehicle > 30 | VVehicle < 180) & DOWN = TRUE, então VVehicle = VVehicle--
- Se VVehicle = 30 & DOWN = TRUE, então VVehicle = VVehicle
- Se VVehicle = 180 & DOWN = TRUE, então VVehicle = VVehicle--
- Se !CCL & DOWN = TRUE, então VVehicle = VehicleSpeed

RESUME
- Se (VVehicle > 30 | VVehicle < 180) & RESUME = TRUE, então VVehicle = VSet
- Se VVehicle = 30 & RESUME = TRUE, então VVehicle = VSet
- Se VVehicle = 180 & RESUME = TRUE, então VVehicle = VSet
- Se !CCL & RESUME = TRUE, então VVehicle = VehicleSpeed

----------------------------------------------CCL----------------------------------------------

SCGND e SCVBAT (VVehicle > 30 | VVehicle < 180)
- Se (VVehicle > 30 | VVehicle < 180) & SCGND & SCVBAT = TRUE, então CCL = TRUE
- Se (VVehicle > 30 | VVehicle < 180) & ClutchSwitch & BrakePedalSts = TRUE, então CCL = TRUE
- Se (VVehicle > 30 | VVehicle < 180) & UP = TRUE, então CCL = FALSE
- Se (VVehicle > 30 | VVehicle < 180) & DOWN = TRUE, então CCL = FALSE
- Se (VVehicle > 30 | VVehicle < 180) & RESUME = TRUE, então CCL = FALSE

SCGND e SCVBAT (VVehicle < 30 | VVehicle > 180)
- Se (VVehicle < 30 | VVehicle > 180) & SCGND & SCVBAT = TRUE, então !AF (CCL = TRUE)
- Se (VVehicle < 30 | VVehicle > 180) & ClutchSwitch & BrakePedalSts = TRUE, então !AF (CCL = TRUE)
- Se (VVehicle < 30 | VVehicle > 180) & UP = TRUE, então !AF (CCL = TRUE)
- Se (VVehicle < 30 | VVehicle > 180) & DOWN = TRUE, então !AF (CCL = TRUE)
- Se (VVehicle < 30 | VVehicle > 180) & RESUME = TRUE, então !AF (CCL = TRUE)

Obs: Necessita de uma ordenação topológica
