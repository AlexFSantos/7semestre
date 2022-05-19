# 7semestre

Projeto do 7 semestre

## para funcionar precisa substituir a cache no começo


# arrumando o plotting
plotting.setup_mpl()

# habilitando o cache
ff1.Cache.enable_cache('/cache') -> aqui

# tirando os warnings do panda
pd.options.mode.chained_assignment = None


## essa parte aqui demora mesmo
# selecionando todos os pilotos
drivers = pd.unique(laps['Driver'])

telemetry = pd.DataFrame()

# telemetria só pode ser um piloto por vez
for driver in drivers:
    driver_laps = laps.pick_driver(driver)
    
    # precisamos pegar a telemetria volta - volta
    for lap in driver_laps.iterlaps():
        driver_telemetry = lap[1].get_telemetry().add_distance()
        driver_telemetry['Driver'] = driver
        driver_telemetry['Lap'] = lap[1]['RaceLapNumber']
        driver_telemetry['Compound'] = lap[1]['Compound']
    
        telemetry = telemetry.append(driver_telemetry)
        
        
## aqui escolhe a volta a ser mostrada
generate_minisector_plot(32, save=True, details=False)
