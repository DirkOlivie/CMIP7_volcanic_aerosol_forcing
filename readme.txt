FILES USED IN NorESM3:
UOEXETER-CMIP-2-2-1_175001-202312_intpwghtavg_v20260105.nc       [timeseries]
UOEXETER-CMIP-2-2-1_185001-202112-clim_intpwghtavg_v20260105.nc  [climatology]



## CMIP7_volcanic_aerosol_wl_interpolater-midpoint.py
	slightly modified :
		modified interpolation : fill_value="extrapolate" replaced by fill_value=(opt_prop_source[:,:,:,0], opt_prop_source[:,:,:,-1])
		modified time_bnds
		contains CAM wavelength-bands
		inputdata directory
		output directory : 
		output filename : always has 'intpmidpoint' in name
		periods to handle : '185001-202112-clim' | '175001-202312'
	to run :
		set period       : '185001-202112-clim' | '175001-202312'  
		set data_version : e.g., 'UOEXETER-CMIP-2-2-1'



## CMIP7_volcanic_aerosol_wl_interpolater-weighted-avg.py
	AIM : interpolated to wavelengths of NorESM (but not yet correct DATES as read by NorESM3)
	METHODS : can work on different datasets
		'175001-202312'              : treating timeseries - no averaging
                '185001-202112-clim'         : use climatology from CMIP7
                '185001-202112-clim-wghtavg' : use climatology which I generated myself
	SLIGHTLY MODIFIED :
		modified interpolation (to extrapolation)
		excluded_lw 
		excluded_band_lw
		function read_cmip7_source_data_v130 : extra argument data_version
		contains CAM wavelength-bands
		input directory : source_dir = '/nird/datalake/NS9560K/noresm3/input4mips/cmip7'
		output directory : output_dir = 'your_output_dir' -> /scratch/olivie/code/python-external/CMIP7_volcanic_aerosol_forcing/output'
		interpolated_filename_part  = 'CMIP7_interpolated' -> 'intpwghtavg'+'_input4MIPs_aerosolProperties_CMIP_'+data_version+'_gnz_'+period
	TO RUN :
		set dataset to start from : '175001-202312'              : treating timeseries - no averaging       [USED !!]
                                            '185001-202112-clim'         : use climatology from CMIP7               [USED !!]
                                            '185001-202112-clim-wghtavg' : use climatology which I generated myself [ONLY USED FOR COMMUNICATION WITH TOMAS AUBRY] 
		set data_version : e.g., 'UOEXETER-CMIP-2-2-1'
	INPUT : input directory : source_dir = '/nird/datalake/NS9560K/noresm3/input4mips/cmip7'
	OUTPUT : output_dir = 'your_output_dir' -> /scratch/olivie/code/python-external/CMIP7_volcanic_aerosol_forcing/output'
	




		
## CMIP7_volcanic_aerosol_time_interpolater-weighted-unweighted-avg.py	
	AIM : converting the original timeseries dataset into climatology
        METHOD : 2 options 'stndavg' | 'wghtavg'
	NEW : but best based on CMIP7_volcanic_aerosol_wl_interpolater-weighted-avg.py
		interpolate_to_wavebands -> interpolate_to_climatology
        	skipped difference between LW and SW
        	avgtype : 'stndavg' | 'wghtavg'
        	nmonths = 12 : always
        NO CHOICE : only works for
                period_clim='185001-202112-clim'
                period_series='175001-202312
	INPUT DIRECTORY : 
	OUTPUT DIRECTORY : '/nird/datalake/NS9560K/noresm3/input4mips/cmip7/'+data_version
	OUTPUT FILES : (they still exist)
		ext_input4MIPs_aerosolProperties_CMIP_UOEXETER-CMIP-2-2-1_gnz_185001-202112-clim-stndavg.nc
 		ssa_input4MIPs_aerosolProperties_CMIP_UOEXETER-CMIP-2-2-1_gnz_185001-202112-clim-stndavg.nc
 		asy_input4MIPs_aerosolProperties_CMIP_UOEXETER-CMIP-2-2-1_gnz_185001-202112-clim-stndavg.nc
 		ext_input4MIPs_aerosolProperties_CMIP_UOEXETER-CMIP-2-2-1_gnz_185001-202112-clim-wghtavg.nc
 		ssa_input4MIPs_aerosolProperties_CMIP_UOEXETER-CMIP-2-2-1_gnz_185001-202112-clim-wghtavg.nc
		asy_input4MIPs_aerosolProperties_CMIP_UOEXETER-CMIP-2-2-1_gnz_185001-202112-clim-wghtavg.nc

INPUT OF ALL THE CODE :
/nird/datalake/NS9560K/noresm3/input4mips/cmip7


OUTPUT OF ALL THE CODE :
/scratch/olivie/code/python-external/CMIP7_volcanic_aerosol_forcing/output/
