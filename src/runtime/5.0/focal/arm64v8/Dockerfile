ARG REPO=mcr.microsoft.com/dotnet/runtime-deps

# Installer image
FROM arm64v8/buildpack-deps:focal-curl as installer

# Retrieve .NET
RUN curl -fSL --output dotnet.tar.gz https://dotnetcli.azureedge.net/dotnet/Runtime/5.0.13/dotnet-runtime-5.0.13-linux-arm64.tar.gz \
    && dotnet_sha512='428adbb6cd564b919333cf18b7245784b6a2e93740e31fb85c4344690519eb88038b220621f199ba2524eef0f4d0fd2e17bbea0851de0d0ec7dec4c092311d10' \
    && echo "$dotnet_sha512  dotnet.tar.gz" | sha512sum -c - \
    && mkdir -p /dotnet \
    && tar -ozxf dotnet.tar.gz -C /dotnet \
    && rm dotnet.tar.gz


# .NET runtime image
FROM $REPO:5.0.13-focal-arm64v8

ENV DOTNET_VERSION=5.0.13

COPY --from=installer ["/dotnet", "/usr/share/dotnet"]

RUN ln -s /usr/share/dotnet/dotnet /usr/bin/dotnet
