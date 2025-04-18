FROM continuumio/miniconda3

# Root: install system packages and create non-root user
RUN apt-get update && apt-get install -y sudo && \
    useradd -ms /bin/bash vscode && \
    echo "vscode ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

# Set working dir and copy environment file
WORKDIR /home/vscode
COPY environment.yml /tmp/environment.yml

# Run Conda setup as root
RUN conda env update -n base -f /tmp/environment.yml && \
    conda clean -afy

# Activate conda base in all shells
RUN echo ". /opt/conda/etc/profile.d/conda.sh" >> /etc/bash.bashrc && \
    echo "conda activate base" >> /etc/bash.bashrc

# Expose Jupyter port
EXPOSE 8888

# Switch to dev user
USER vscode
