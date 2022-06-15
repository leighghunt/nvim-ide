# Docker file for Neovim Typescript development.
#
# @author Leigh Hunt

# Base Neovim image.
FROM mashmb/nvim:dev

# Install Typescript SDK.
RUN apt-get update && apt-get -y install watchman wget

# Install DotNet - for ARM must be from source
# # https://docs.microsoft.com/en-us/dotnet/core/install/linux-ubuntu
# RUN wget https://packages.microsoft.com/config/ubuntu/22.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
# RUN sudo dpkg -i packages-microsoft-prod.deb
# RUN rm packages-microsoft-prod.deb
# https://docs.microsoft.com/en-us/dotnet/core/install/linux-debian
RUN wget https://packages.microsoft.com/config/debian/11/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
RUN dpkg -i packages-microsoft-prod.deb
RUN rm packages-microsoft-prod.deb

# Install the SDK
RUN apt-get update; \
 apt-get install -y apt-transport-https && \
 apt-get update && \
 apt-get install -y dotnet-sdk-6.0

# Install Node.js debugger adapter.
RUN cd /root/.config/nvim/plugins/vimspector && python3 install_gadget.py --force-enable-node

# Copy Neovim configuration files.
COPY ./config/ /root/.config/nvim/

# Avoid container exit.
CMD ["tail", "-f", "/dev/null"]
