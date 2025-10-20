Nvidia HPC:
	module load nvhpc/25.3
	ip link show
	mpirun -np 1 -x OMP_NUM_THREADS=20 -x HCOLL_MAIN_IB=lo -x UCX_NET_DEVICES=lo

OpenMP + OpenMPI:
	module load mpi/openmpi-x86_64
	ip link show
	mpirun -np 1 -x OMP_NUM_THREADS=20 -x HCOLL_MAIN_IB=lo -x UCX_NET_DEVICES=lo

vc-relax calculation:
	pw.x < csi_vc_relax.in > csi_vc_relax.out

scf calculation:
	pw.x < csi_scf.in > csi_scf.out	
	pw.x < csi_nscf.in > csi_nscf.out

band calculation:
	pw.x < csi_bands.in > csi_bands.out

band post-processing:
	bands.x < csi_bands.pp.in > csi_bands.pp.out
	plotband.x < csi_plot_bands.in > csi_plot_bands.out

phonon bands & dos calculations:
	scf first

	ph.x < csi_ph.in > csi_ph.out
	q2r.x < csi_q2r.in > csi_q2r.out

	matdyn.x < csi_matdyn_bands.in > csi_matdyn_bands.out
	plotband.x < csi_plot_ph_bands.in > csi_plot_ph_bands.out

	matdyn.x < csi_matdyn_dos.in > csi_matdyn_dos.out

dos calculation:
	pdos.x < csi_pdos.in > csi_pdos.out
